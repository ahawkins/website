---
title: "Codefresh"
description: |
  Codefresh is a hosted or hybird deployment pipeline tool. Best
  practices and gotchas for writing pipelines.
date: 2021-03-14T22:29:23-10:00
---

Codefresh is a hosted and hybrid deployment pipeline solution. It may
be used for testing and or deploying software. All steps in the
pipeline run as Docker containers. Users can create reusable custom
steps as well. Users can opt for the hosted version or host their
runner on their own Kubernetes cluster.

## Related Links

- [Next Gen Deployments at Skillshare Webinar][skillshare webinar]: A
  webinar I hosted for Codefresh sharing my experience building
  deployment pipelines for Skillshare.

## Gotchas

### Hooks and Steps Do Not Share Env Vars

_Last encountered: Jan 2021_

[Codefresh Hooks][hooks] appear to act like regular steps. You may
consider using a hook and `cf_export` to set variables for all future
steps in the pipeline. This **does not work**. Hooks and steps do not
share the same context. In fact, they don't even have access to
pipeline variables. Variables must be passed in directly to hooks.

### Custom Steps Use Prerelease Versions

_Last encountered: March 2021_

[Codefresh Steps][steps] use semantic versioning. If a pipeline step
version is not declared then the "latest" version is used.
Unfortunately "latest" includes prerelease versions.

Consider this step definition with the current version of `1.0.0.`

```
foo:
  type: myorg/custom
```

Then you release `myorg/custom:2.0.0-beta1`. The `foo` step will now
use the `2.0.0-beta1` release even though it's not considered a stable
release.

There is no known solution pinning steps to always use the latest
"stable" version. Codefresh has the "incubating" or "stable" channels
for each step but these do not apply to releases. They only apply to
how they're presented in the UI.

### Conflicting Step & Pipeline Services

_Last encountered: March 2021_

[Codefresh Services][services] may be declared at the pipeline level
(they run for all steps) or at the step level (run for a single step).
These are mutually exclusive. If you delcare pipeline services and
step services then _only_ the step services will run for that step.

### Undefined Variable Literals

_Last encountered: March 2021_

[Codefresh Variables][variables] may be referenced using `${{NAME}}`
in the pipeline definition or as environment variables in commands
(`$NAME` or `${NAME}` depending on your shell and/or preference).

Say you reference `${{FOO}}` somewhere in the pipeline definition. If
`FOO` is set then value is interpolated. If `FOO` is not set then
value is left as a literal `${{FOO}}`. This is especially annoying
when dealing with optional variables (say those that may be set on
different triggers).

You'll need to check if the value matches a variable format to decide
if a true value is provided.

Here's an example:

```
if echo "${FOO}" | grep -qE '\$\{\{.+\}\}'; then
  echo "FOO not provided"
else
  echo "FOO=${FOO}"
if
```

This is only possible inside commands. There is no way to check the
variable in the pipeline definition. You may be able to do this with
conditional steps though.

### Custom Step Environment Variables

_Last encountered: March 2021_

Pipeline variables outside the system provided variables **are not**
automatically set on custom steps. I guess this is because of security
reasons? If this were true then any step would see all variables
(including secrets). This would make it possible for attacks to write
steps like `env | upload-to-remove-server`. Anyway the end result is
that you cannot assume custom steps have access to pipeline
environment variables.

There is a workaround. You can use the `stepTemplate` to capture env
variables and set them in the `environment` list. You'll have to deal
with the other gotcha that undefined variables **are not
interpolated**. Here's an example:

```
stepsTemplate: |-
  main:
    name: example
    image: example
    environment:
      - KUBE_CONTEXT=[[ default "${{KUBE_CONTEXT}}" .Arguments.KUBE_CONTEXT ]]
```

This template takes the `KUBE_CONTEXT` argument or uses the
`KUBE_CONTEXT` variable from the pipeline. If the `KUBE_CONTEXT` is
not set then the step will receive a literal `${{KUBE_CONTEXT}}` for
`KUBE_CONTEXT`. Step authors are advised to always validate env vars.

### Exporting Environment Variables in Steps

_Last encountered: April 2021_

Exporting environment variables in your own steps and custom steps is
different. The docs refer to `cf_export`. This is for your exporting
env vars in your own steps. Do not use this when writing custom steps.
Custom steps should echo `export FOO=bar >> /meta/env`. Apparently the
`/meta/env` is a special file that Codefresh reads when authoring
custom steps.

### Pipeline Template Variable Limitations

_Last encountered: March 2021_

You may assume that you can reference variable using the `${{var}}`
syntax anywhere in the pipeline YAML file. This is **not** the case.
These "pipeline" variables (or whatever they're called) do not work
everywhere. They work _most_ places.

Here's an example.

```yaml
steps:
  build:
    type: build
    # ....

  run:
    image: foo
    commands:
      - echo ${{build}}
```

This does not work. The `${{build}}` step variable may only be used in
certain places in the YAML file.

[services]: https://codefresh.io/docs/docs/codefresh-yaml/service-containers/
[steps]: https://codefresh.io/docs/docs/codefresh-yaml/steps/
[variables]: https://codefresh.io/docs/docs/codefresh-yaml/variables/
[hooks]: https://codefresh.io/docs/docs/codefresh-yaml/hooks/
[skillshare webinar]: https://codefresh.io/events/next-gen-deployments-skillshare/
