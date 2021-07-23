---
title: "Cloudflare Workers"
author: "Adam Hawkins"
date: 2021-07-23T11:25:02-10:00
---

[Cloudflare Workers][workers] provide an execution environment that
allows you to create entirely new applications or augment existing
ones without configuring or maintaining infrastructure. Basically, you
can use Javascript to intercept and augment incoming requests before
they hit your origin.

This guide covers building a deployment pipeline using the official
[wrangler]. Wrangler is the official tool from Cloudflare to develop,
build, and deploy workers. It has similar functionality [serverless][]
framework.

JS workers are structured differently than AWS Lambda functions (and
perhaps other FaaS providers). AWS Lambda functions _export_ a
function handler. This makes them much easier to develop and tests.
Unfortunately Cloudflare Workers execute in the global context. This
requires a little shimming for automated testing.

Wrangler provides a "dev" environment. This transparently deploys the
worker to Cloudflare's dev cloud and proxies it back to localhost.
This is your "F5 driven development" model. However, this has nothing
to do with automated testing.

Wrangler also provides a `publish` command to deploy workers. It also
supports an `--env` option for specific configurations in different
environments.

## Automated Testing

I recommend using [jest][] for Javascript testing. Jest includes hooks
for simulating Cloudflare's execution environment. You'll need to
include `node-fetch` and use `setupFilesAfterEnv` to configure globals
and anything else Cloudflare injects into the environment. My guess is
that adding classes and functions around `fetch` is enough.

**First**, write the handler so it works with Node.js. This snippet
checks for the CommonJS `module` for determining Cloudflare vs Node.js
runtime.

```javascript
async function handleRequest(request) {
  // do your stuff
}

if (typeof module === "undefined") {
  addEventListener("fetch", (event) => {
    event.respondWith(handleRequest(event.request));
  });
} else {
  module.exports = handleRequest;
}
```

**Second**, use Jests `setupFilesAfterEnv` to assign `Request` and
`Response` globals and mock `fetch`.

```javascript
// setup.jest.js

const { Request, Response } = require("node-fetch");

// see gotchas
Response.redirect = function (url, status = 302) {
  return new Response(null, {
    headers: {
      location: new URL(url).toString(),
    },
    status,
  });
};

// Assign whatever globals Cloudflare injects into the environment
global.Request = Request;
global.Response = Response;

// mock fetch so no network traffic ever occurs
beforeEach(() => {
  global.fetch = jest.fn();
});
```

Now you can write simple tests like this:

```javascript
const worker = require("./index");

test("example", async () => {
  await worker(new Request());

  expect(fetch).toHaveBeenCalled();
});
```

## Deployments

Deployment's are simple `wrangler publish` commands. I recommend
introducing a specific `production` configuration into
`wrangler.toml`. Cloudflare does not support multiple "environments"
per-say. You can emulate that by changing the configured route
listeners. Note that `wrangler` automatically appends the environment
to the worker name in Cloudflare.

The pipeline should [authenticate with environment
variables](https://developers.cloudflare.com/workers/cli-wrangler/authentication#using-environment-variables).

## Gotchas & Caveats

- `node-fetch` version 2.6 does not include the `Response.redirct`
  function. This is included in version 3.0 which is currently in
  Beta at the time of this writing.
- `wrangler` does not support multiple workers inside a single
  project. You'll need to create multiple folders (with relevant
  `package.json`, `wrangler.toml`, etc) for all workers you'd like to
  keep in the same repository.
- Cloudflare workers and `wrangler` are not competitors to
  `serverless`. These are apples to oranges. If you've worked with
  `serverless` you'll find that workers + wrangler is a paired down
  setup.

[workers]: https://developers.cloudflare.com/workers/
[wrangler]: https://github.com/cloudflare/wrangler
[serverless]: https://serverless.com
[jest]: https://jestjs.io/
