---
title: "curl(1)"
author: "Adam Hawkins"
date: 2021-03-30T21:44:21-10:00
tags:
  - shell
  - bash
toc: true
description: |
  Effective curl usage with examples, recommendations, and gotchas
---

> curl -- transfer a URL

`curl` is one of the OG commands. The best way to learn `curl` is by
example. There are two primary styles: interactive and
noninteractive.

Interactive mode means someone is manually entering `curl` commands.
Noninteractive means used in a script. Noninteractive
implies `set -euo pipefail` in this guide. That means in a
noninteractive mode, we want curl commands to fail (exit non-zero) if
the request does not work _and_ print an error for transparency.

## Examples

```
# write the contents to standard out
$ curl https://example.com
```

```
# write the contents to a file (--output/-o)
$ curl -o sample.html https://example.com
```

```
# print request and response headers
$ curl -v https://example.com
```

```
# supress progress information (--silent/-s)
$ curl --silent https://example.com
```

```
# Make a URL encoded POST request
$ curl --data-urlenencode foo=bar https://example.com
```

```
# Make a JSON POST request
$ curl \
  -H 'Content-Type: application/json` \
  --data-binary '{"foo":"bar"}' \
  https://example.com
```

```
# Make a request in a script (i.e non-interactive mode) that fails
with an error if unsuccessful
$ curl -fsSL https://example.com
```

## Common Options

`-o`, `--output`
: Write the response body to this location. `curl` outputs to standard
out by default.

`-s`, `--silent`
: AKA: do not output anything. Disables the progress bar.

`-f`, `--fail`
: Do not output anything and exit non-zero on server errors.

`-S`, `--show-error`
: Use with `--fail` to print an error to standard error

`-L`, `--location`
: Follow a redirect

`-H HEADER`
: Set a Header. May be specified multiple times.

`-X METHOD`
: Set the HTTP method

`-d key=value`, `--data key=value`
: Set `key` to the URL encoded value

`-u <user:password>`, `--user <user:password>`
: Set an HTTP username and password. Either or both my be specified
(`just-user:` or `:just-password`).

## Recommendations

- Use `-fsSL` in all scripts
- Control output with `-o`
- Prefer `--data-urlencode` instead of `-d` or `--data`
- Prefer `-u` or `--user` instead of manual `-H` authorization headers
  when possible

## Gotchas

### --data vs --data-urlencode

You'll see many examples like `curl -d foo=bar https://example.com`.
The `-d` or `--data` option **does not** URL encode the value. This
typically works for simple values but leaves new users assuming that
`-d` is the way to send POSTS with data. I recommend using
`--data-urlencode` over `-d` or `--data` because commands with these
options, in my experience, typically work with machine or user
provided data; thus they _may_ need URL encoding to send correctly.
Put it another way: how often are you working with previously URL
encoded values? If you're like me then answer is virtually never.

### Data Options Do Not Support Nested Objects or Arrays

You may be thinking something like `curl -d foo[bar]=baz` works. It
doesn't. If you need to send complex data then either use JSON
(through `-H 'Content-Type: application/json` and `--data-binary`) or
find a way to encode data outside curl and use with `--data @file.txt`.

Odds are if you hitting this, then you're pushing up against the
limits of `curl` for your use case.

### No Failed Responses to Standard Error

**tl;dr**: `curl -fsSL` is the best you're gonna get for
noninteractive uses.

I want my `curl` commands to behave like this: If the response is a
200 then output as directed; if not then exit non-zero and print the
response body to standard error.

This behavior is not possible to my knowledge.

Using `--fail`, `--silent`, `--show-error` meet the first requirement.
However if the request fails, `curl` outputs something like `Server return 403 (exit 22)` to standard error. This information is helpful
but not entirely. The response body is _especially_ useful in this
case because it may indicate _why_ the response is 403.

This may be possible if `curl` could write responses as directed (by
using `-o` or `--output`) _and_ to stderr. This is not possible. The
response body may only be handled with `-o` or `--output`. So if you
want to see the response body on error _and_ exit non-zero then there
is no way to accomplish this.

If you _really_ need this behavior then you need to use the
`--write-out` in combination with `-o` and omit `--fail`. This allows
you to write the status code and body separately. They can be checked
and handled separately.
