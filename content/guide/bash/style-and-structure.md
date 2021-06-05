---
title: "Bash Bootcamp: Elements of Style & Structure"
author: "Adam Hawkins"
date: 2021-06-04T22:39:56-10:00
tags:
  - shell
  - bash
summary: |
  The unofficial Bash strict mode and recommend program structure
---

I advocate applying best practices to problems of all sizes. This may
be a small demo script, but if one always applies best practices then
this will become second nature. Bash is no different. Best practices
are especially important because of the inherit quirks. The [Google
shell style guide][style guide] is an excellent starting point. It
mentions style (things like quoting, variable definitions, naming,
etc) and structure. Together these two things will keep on the happy
path. This book makes some additions that I've found useful in
practice.

1. Always use the unofficial strict mode
2. Run everything through [shellcheck][]
3. Use variable indicators
4. Define a usage function
5. Define a main function

The unofficial strict mode is the most important of the whole list.
Bash has many options. The most important, in my opinion, are off by
default. These options are controlled by the `set` built in command.
This line follows the shebang (`#!`) in every bash program: `set -euo pipefail`. This sets the following options.

`set -e`
: Exit if any command fails (exits non-zero). In
practice this means misspelled arguments, missing files, or anything
else that could go wrong is treated as an exit case instead of just
continuing on.

`set -u`
: Fail when an undefined variable is used. Bash treats
unassigned variables as blank strings by default. This is an annoying
behavior that makes programs hard to debug. A program should
never have undefined variables. This setting also requires the program
to handle cases where the value may be blank, which is good all around.

`set -o pipefail`
: Fail if any step in a pipeline fails. This is
another default annoyance. Assume the program calls `foo | bar | baz`.
Say bar fails. Out of the box, Bash will continue on as if this is OK.
This option tells the shell to exit if any part of the pipeline fails.

These three options will make Bash programs feel like most programming
languages: blowing up on stupid mistakes and failures. Now with that
out the way we can get back to sanity.

[Shellcheck][] is a godsend for Bash programmers. Bash has many quirky
behaviors that make it behave less like high level languages. This is
frustrating because it creates fiction and things may break in weird
or unexpected ways. Shellcheck solves 80% of the pain points through
static analysis. It picks up things like misspelled variables,
improper quoting, unused variables, uninitialized variables, and much
more. Shellcheck is as close as you are going to get to a compiler for
Bash programs. All the examples in this book pass shellcheck on
default settings from this point on.

Now for the next point: variable indicators. Bash allows you do many
things with variables which will be touched on later. We also saw that
a variable can be inserted (and interpolated) into a string anywhere.
However how does the interpreter know where a variable name begins and
ends? Bash generally does a very good job of making this transparent
but you may hit a problem. The correct way, is to use braces to
indicate variable names. This removes any confusion and makes it easy
to use parameter substitution (`${1:-}`) at any point in the program.

The next two points go together. Both are structural points and are
designed to ensure the program does not grow into a single chunk.
Creating functions is also a great way to ensure separation and make
the program more comprehensible.

Time to update the previous example so it fits our elements of
structure and style.

```bash
#!/usr/bin/env bash

set -euo pipefail

usage() {
  echo "USAGE: ${0} NAME" 1>&2
}

main() {
  local name="${1:-}"

  if [[ -z "${name}" ]]; then
    usage
    return 1
  fi

  echo "Hello ${name}"
}

main "$@"
```

Let's unpack the example a bit. Defining functions is straight
forward. There are two functions: `usage` and `main`. The `main`
function uses a local variable `name` with `local` (according to the
style guide). This line also uses parameter substitution to insert a
blank value for a missing arguments. Using `set -u` requires this.
This way running `./hello-world` will not exit with an undefined
variable error, but print usage and exit. The if conditional now calls
the `usage` function. `return` replaces `exit`. This is important!
`exit` will exit the process which is not a problem when there are no
functions. However, functions should always use `return`. The program
shouldn't exit because a function completed right? Finally `main` is
called on the last line. `$@` is a special variable. It refers to all
given arguments. Phew, quite a bit of changes! However this structure
is portable to programs of all shapes and sizes. It will be second
nature to you once you get in the habit. It was actually hard for me
to write the first example because I was breaking my habit! Time to
quickly go over what was covered:

1. Declaring functions and handling arguments
2. Conditionals and empty value checking
3. Enabling sane defaults (unofficial "strict mode")
4. Proper structuring

This information has hopefully prepared you to enter the realm of
bash programming.

[style guide]: https://google.github.io/styleguide/shell.xml
[shellcheck]: https://www.shellcheck.net/
