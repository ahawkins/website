+++
date = 2017-08-02T00:00:00Z
summary = "Anyone can run a command like helm install $MARKET and everything will work as expected. Preconfigured versions for different STAGE values are communicated through different semantic versions. "
tags = ["saltside", "kubernetes", "helm"]
title = "Building Saltside's Helm Chart"
aliases = [ "/blog/2017/building-our-helm-chart/" ]
+++

Saltside recently migrated production applications to Kubernetes using
Helm to deploy the application. This post describes how we built our
chart to fit Saltside’s unique business requirements.

Saltside makes classifieds (user posted ads, not secret information)
sites. We operate in multiple markets:
[Tonaton.com](https://tonaton.com), [Bikroy.com](https://bikroy.com),
[Efritin.com](https://efritin.com), and [Ikman.lk](https://ikman.lk).
I’ll refer to this as `MARKET` going forward. I suggest you checkout
the sites. You’ll notice they look and feel the same. That’s by
design!

Market infrastructure is deployed, scaled, and operated separately
from the others. This ensures each market’s infrastructure scales
correctly for load and other requirements while guarding against
failures propagating to others. Deploying separately requires
different configuration for each `MARKET`. Configurations must be
tested in different stages in the deployment pipeline. Example stages
are production or uat. I’ll refer to this as `STAGE` going forward.

Naturally this propagates down to individual codebases. Each code base
must support different `MARKET` and `STAGE` values. Our product is
composed of ~20 independent code bases that may themselves be composed
of multiple deployed processes (such as a thrift server, web server,
or working off messages in queue). I’ll use `COMPONENT` to refer to
components or code bases and `PROCESS` to refer processes inside each
`COMPONENT`.

You may be thinking “this sounds like _a lot_ of stuff!” You’re right.
_It is_. The total possible configuration is `MARKET` _ `STAGE` _
`COMPONENT` \* `PROCESS`. You can learn more about our previous setup
in [my talk at DevOps Days India
2016](https://www.youtube.com/watch?v=VcOx21_e6fA). This the jumping
off point for discussing our Kubernetes solution.

## Requirements

The big idea is that we’ll move from independently configured and
deployed `COMPONENT` to centrally configured and deployed mono-repo.
The implementation is no surprise from the title. The entire product
(all configuration for `MARKET`, STAGE, `COMPONENT`, and `PROCESS`)
are wrapped up in a single repo that builds [Helm](http://helm.sh)
charts. I’m not going into the reasons why we chose Helm. There are
plenty of articles, talks, and presentations on what Helm is and what
it can do. Let’s move onto specifics we need from our Helm chart.

### Market, Stage, Component and Process Configuration

`MARKET`, `STAGE`, `COMPONENT`, and `PROCESS` specific environment
variables and secrets. There is a hierarchy between those 4 values.
`MARKET` is the most general and `PROCESS` is the most specific. A
specific `COMPONENT` may need different environment variables
depending on `MARKET` or `STAGE`. `PROCESS` may need the same. Here’s
a concrete example. The same `BUGSNAG_API_KEY` may apply to all
`PROCESS` inside a given `COMPONENT`. However something like
`EXTERNAL_REDIRECT_URL` may need different values depending on
`MARKET` or `STAGE`.

### A Single Values File

No separate values files or requirements to pass `-f` or `--set` on
`helm install` or `helm upgrade`. There are too many possible
configurations. That also forces engineers to mange these files or
pass in command line flags is simply unmanageable in our problem
domain.

### Encrypted Secrets Values

Our current solution is subpar in this area so we’d like to, at a
minimum, encrypt sensitive data that’s committed to SCM.

### Preconfigured Charts for MARKET and STAGE

This is somewhat a follow up to the previous point. The idea here is
that anyone can run a command like `helm install $MARKET` and
everything will work as expected. Preconfigured versions for different
`STAGE` values are communicated through different semantic versions.
This requirement opens up many use cases such as automatic environment
creation from topic branches or allowing any engineer to stand up test
environments against arbitrary configurations.

### Easier or Better than our Current Solution

Different COMPONENT and PROCESS configurations should be as easy as
current solution or easier. This one is subjective so here’s some
background. Different COMPONENT have roughly the same shape. All
COMPONENT values share the same Docker image. Different PROCESSS run
as different containers using that Docker image. This may require a
different command, ports, environment variables, or other things. This
generally boils down to expressing configuration at _our_ abstraction
level rather than Helm’s.

### Deployable to any Kubernetes Cluster

The chart should be deployable on any Kubernetes cluster. This means
it should be self contained, specifically it should contain an image
pull secret for access to private Docker images.

Those are the high level requirements around chart. Let’s see how this
requirements drive the implementation.

## Implementation at 10,000ft

The requirements dictate a single values.yaml file and a build process
that can spit out preconfigured charts for different M and S values.
Here’s what this looks like for us:

- Everything declared in values.yaml with a _ton_ of YAML anchors
  (more on that later)
- `script/lint-values` tests `values.yaml` for correct semantics.
  Example: each combination of M, S, C, and P have declared
  environment variables (so range in chart templates works as
  expected).
- Secret values kept in a `secrets.yaml` managed with
  [git-crypt](https://www.agwa.name/projects/git-crypt/). We initially
  tried using Ansible vault but aborted that effort. More on that
  later as well.
- A parameterized build script that injects the correct values for
  `MARKET` and `STAGE` _into_ `values.yaml` _before_ building the
  final chart. The production `STAGE` produces a chart named
  `MARKET-VERSION`. The sandbox `STAGE` produces a chart named
  `MARKET-VERSION.betaN`. Any `STAGE` is supported through different
  version modifiers. The versioning information is determined by the
  commit and git branch.
- Chart templates expect a specific structure in `$.Values` to
  generate each Service, Deployment, and Pod etc. This allows defining
  everything about `COMPONENT` and `PROCESS` in `values.yaml` without
  creating new templates.

In short, our mono repo is a template for producing `MARKET * STAGE`
Helm charts. Let’s dive into implementation specifics.

## Templates & Values

The chart templates are straight forward. There is one template for
Service, Deployment, and Secret. Each template produces multiple
resources (separated by ---) in YAML from range functions over various
`$.Values`. The charts essentially loop over
`$.Values.applications[].containers[]` (where application refers to
`COMPONENT` and containers is `PROCESS`). One Deployment is created
for each `COMPONENT` and `PROCESS` combination because this is how
_our_ system scales. One Service is generated for each `COMPONENT`
with ports for each `PROCESS`. “Our” is emphasized on purpose. Your
application may be different.

Our `values.yaml` and `secrets.yaml` rely on YAML anchors. This is
especially useful for “overriding” the
`MARKET/STAGE/COMPONENT/PROCESS` hierarchy. Initially this started out
in in the templates (one loop for each). It was easier to move
everything into values using YAML anchors.

The `values.yaml` defines images for each `COMPONENT` value; as well
as common things like `MARKET` and `STAGE` values. There are many
shared environment variables (like `MARKET`, `STAGE`, `RACK_ENV`, or
`NODE_ENV`) that are defined as anchors and appended to. Let’s look at
the main anchors. Anchors are prefixed with \_ to prevent accidental
clashes with real variables. They are also annotated with comments so
readers know that these are not intended for direct use, but only
referenced later in the file. Here is an example:

```
_anchors:
  common_env: &COMMON_ENV
    APP_VERSION: "${CHART_ID}"
    APP_ENV: "${CHART_STAGE}"
    NODE_ENV: "${CHART_STAGE}"
    RACK_ENV: "${CHART_STAGE}"
    RAILS_ENV: "${CHART_STAGE}"
    MARKET: "${CHART_MARKET}"
    STATSD_URL: "udp://localhost:8125"
    LOG_LEVEL: info
    # TODO: AWS variables
```

The `${VARIABLE}` is special. That’s _inserted_ by the build process
with [envsubst](https://linux.die.net/man/1/envsubst). I’ll cover that
later on. This anchor is reused in each `STAGE` and `COMPONENT`
declaration as shown below:

```
env:
    admin_service:
      production: &ADMIN_SERVICE_PRODUCTION_ENV_VARS
        <<: *COMMON_ENV
      sandbox: &ADMIN_SERVICE_SANDBOX_ENV_VARS
        <<: *COMMON_ENV
        # FIXME: This is wrong!
        APP_ENV: development
        AWS_ACCESS_KEY_ID: foo
        AWS_SECRET_ACCESS_KEY: foo
```

Injecting `COMMON_ENV` anchor into the `COMPONENT * STAGE` context is
easy as well as adding new values (in the sandbox `STAGE` in this
example). That `COMPONENT * STAGE` configuration is assigned a new
anchor name which can be customized by `MARKET` or `PROCESS` later on.
Here’s an `MARKET` example:

```
env:
  admin_service:
    production:
      bikroy:
        <<: *ADMIN_SERVICE_PRODUCTION_ENV_VARS
      ikman:
        <<: *ADMIN_SERVICE_PRODUCTION_ENV_VARS
      tonaton:
        <<: *ADMIN_SERVICE_PRODUCTION_ENV_VARS
      efritin:
        <<: *ADMIN_SERVICE_PRODUCTION_ENV_VARS
    sandbox:
      bikroy:
        <<: *ADMIN_SERVICE_SANDBOX_ENV_VARS
      ikman:
        <<: *ADMIN_SERVICE_SANDBOX_ENV_VARS
      tonaton:
        <<: *ADMIN_SERVICE_SANDBOX_ENV_VARS
      efritin:
        <<: *ADMIN_SERVICE_SANDBOX_ENV_VARS
```

It’s not the prettiest but it works. It removes effort for shared
configuration and makes it easy override all levels in the hierarchy.
This same structure applies to `secrets.yaml`.

Here’s an example `COMPONENT` and `PROCESS` configuration from
values.yaml:

```
    - name: image_service
      tier: thrift
      service_type: ClusterIP
      containers:
        - name: thrift
          command:
            - "thrift-server"
          ports:
            container: 9090
            service: 9090
          livenessProbe:
            initialDelaySeconds: 5
            tcpSocket:
              port: 9090
          resources:
            sandbox:
              requests:
                memory: 128Mi
            production:
              requests:
                memory: 128Mi
                cpu: 50m
              limits:
                memory: 128Mi
                cpu: 100m
```

We mix custom structures and existing Kubernetes ones (like
livenessProbes inside resources). This works well because data may
directly dumped into the manifest.

This gist is our complete deployment template. That there are things
that I’m not going to describe in this post. Note the use of index in
combination with `$.Values.market`, `$.Values.stage`, and
`$.Values.topology.pods`. Also note that generating JSON init
containers is quite _strange_ inside YAML since YAML is white space
sensitive but JSON requires delimiters.

{{< gist "ahawkins" "22f92bc2431f2a3172a0bce6ca48ae10" >}}

Kubernetes Services are declared through a combination of custom data
structures and previously shown `COMPONENT` and `PROCESS`
configuration.

## Repo Organization & Building

I find this section the most interesting personally since it
demonstrates what you can do with Helm when you throw some Bash into
the mix. It requires a bit of funkiness to get everything to work.
I’ll touch on those the most because they highlight curious choices in
Helm chart packaging.

Here’s the tree:

```
.
├── Makefile
├── README.md
├── VERSION
├── chart
│   ├── charts
│   └── templates
│       ├── _helpers.tpl
│       ├── app_deployments.yaml
│       ├── app_services.yaml
│       ├── sandbox.yaml
│       ├── secrets.yaml
│       └── smoke_test.yaml
├── config
│   ├── Chart.yaml
│   └── values.yaml
├── script
│   ├── await-release
│   ├── build
│   ├── ci
│   │   └── test
│   ├── clean-releases
│   ├── lint-manifest
│   ├── lint-values
│   ├── package
│   ├── publish
│   ├── test-chart
│   ├── test-release
│   └── yaml2json
├── secrets.yaml
```

## Building

make coordinates the entire process. `/chart` and `/config` are the
most relevant directories for this section. `/chart` contains files
that _are not_ parameterized and may be copied directly into the final
output directory. `/config` contains files that _are_ parameterized so
each must pass through `envsubst` before coping into the final output
directory. This is where `${MARKET}` etc is inserted into the final
values.yaml file.

`script/build` coordinates the process. It determines the correct
`VERSION` along all other template variables, creates a specifically
named directory for the chart, copies over everything in `/templates`,
templates everything in `/config` and dumps that into the output
directory. It’s shared in its entirety:

{{< gist "ahawkins" "de374928d18d5c13245e9086126ee498" >}}

You’ll also notice chart our versioning semantics coded into that
file. Astute readers will notice that this script does not package or
publish the chart. This script only prepares the directory. That is
enough to install the chart for testing. Other scripts produce the
final.tgz archive and upload to our internal chart repository. There
is nothing interesting in those script. They accept a directory as an
argument and call the various helm commands.

This approach seems is working well enough for our production
continuous delivery pipeline. The CD pipeline is a entire post in
itself. Check back in the future for all the details once all the
kinks are sorted out. I want to close out this post by discussing
things we tried that didn’t work out.

## What Didn’t Work

- Ansible vault for secrets. Internally we use Ansible to automate
  processes and glue various workflows together. We did not want to
  commit secrets in plain text to source control, but we could accept
  encrypting them in source control. Ansible vault was a natural fit
  for us. It worked in the beginning then we hit increased friction
  levels beyond the dev stage. We generated a Kubernetes Secret using
  Ansible templates and variables. The chart required a
  `$.Values.secret_name`. This meant secret must exist in the
  cluster(s) where the chart would be installed on. This became more
  problematic as we have multiple Kubernetes clusters for different
  stages (namely production & non-production). This also opened up a
  question of what to do if the chart itself failed tests? The secret
  would need to be deleted from the clusters. That is possible but
  it’s an avoidable problem. Everything became much easier when
  switched to git-crypt which made the chart self-contained. I advise
  teams adopting Helm start and continue with git-crypt until it
  becomes a pain point.
- Duplicating configuration in templates. Notice the Deployment
  template (naturally) defines the template pods and their init
  containers. The init containers use the same Docker image as
  `COMPONENT` to run init `PROCESS`. Each `PROCESS` generally requires
  the same set of configuration values (such as `COMPONENT` specific
  values like `MYSQL_URL` or `MARKET` or `STAGE` global values).
  Previous versions duplicated generation in different parts of the
  templates. Things became much easier by moving things into
  values.yaml through YAML anchors. I doubt other teams will encounter
  problems of this scope. Regardless it’s an interesting approach to
  keep in your back pocket.
- This is tangentially related to the chart but I think it’s important
  to discuss since it impact the chart’s usability. Initially we
  wanted to pre-authenticate all cluster nodes to our Docker registry.
  We did this through updated the default ServiceAccount to also use a
  custom image pull secret. This seemed like a good idea in the
  beginning, but turned out to be a bad one when it came down to it.
  All this did was introduce more pre-reqs to _where_ the chart could
  be installed. In the end it was easier to create an image pull
  secret as part of chart (also not an issue since git-crypt manages
  our plain text secrets) and use that in all the templates. This was
  another step in making the chart more self contained.
- The chart’s flexibility correlates with the internal application’s
  (`COMPONENT` and `PROCESS`). Our process currently has two stages:
  production and sandbox. Unfortunately our code bases are in various
  stages of being completely configured by environment variables
  and/or command line options. We cannot easily introduce a new stage
  because many code bases hard coded logic on something like
  `NODE_ENV` or `RACK_ENV`. This is reminder that hard coding
  conditional is an anti pattern and should be avoided.

## What’s Next?

We plan for future posts documenting our test strategy, workflow
around the chart, and continuous delivery (and hopefully deployment!)
processes. Stay tuned for more information. Also don’t hesitate to
leave a comment or ask a question. You can also find the SRE team on
the Kubernetes slack in #helm-users, #helm-dev, #in-users, and #kops
if you want to chat with us.

Good luck out there and happy shipping!
