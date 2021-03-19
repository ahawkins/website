---
title: "Bash Bootcamp"
summary: Bash for total beginners.
date: 2016-06-07
toc: false
tags:
  - bash
  - programming
  - tutorial
---

I decided to write this because over the past year I slowly became a
competent Bash programmer. This made more effective than anything else
since learning TDD. Why is that? Bash is everywhere. If you do
infrastructure engineering, operations work, or sys-admin things then
you'll encounter bash on a day to day basis. If you're a normal
developer you come across bash as it's the default shell on pretty
much anything with a terminal. Maybe you don't write bash programs,
but you type things into a shell everyday. This is a single line
program. Installed some software from the internet these days? You've
probably seen `curl` piped to `bash`. Bash is like the force. It is
the power the surrounds us and binds our computers together, master it
and you'll become more powerful than you'll ever imagine. It happened
to me.

Our team switched to use `make` to build our projects. Building
project slowly became more complex. Single line statements in the
`Makefile` where no longer enough. Logic and some pipelines started to
become extracted into executable scripts. More complex logic revealed
the magic of core commands such as `find`, `grep`, and `xargs`.
Scripts grew and became more well structured. We distributing tools
written completely with bash & various supporting commands. Our
deployment infrastructure required us to create executable commands to
start our processes. Slowly things like argument parsing, subcommands,
and more complex things revealed themselves. I took all this knowledge
and created new utilities for my own shell. Personal tasks such as
managing my music library or photos where easily and quickly solved by
stringing together some commands and custom scripts. I was more
productive and empowered. The simple magic of standard in, standard
error, standard out, pipes, redirection, and the command line revealed
itself to me.

This article summarizes the things I learned along the way. It is not a
seminal masterwork encompassing everything you need to know. Instead
it's results oriented. I assume you're a technical person with
programming experience so you understand things like control
structures, input validation, testing, and function calls. However,
I'll assume, you don't know how to do _confidently with Bash_. This
book will remove some of the mystery from black magic known as "shell
scripting". You'll learn that the dark is art is just some
conditionals top of a bunch of powerful commands. So join me on a fast
paced journey into Bash. I swear it won't take you as long as it took
me.

## Hello World!

Every programming book starts off with the classic "Hello World"
program. The program simply prints the text "Hello World". This is
simple enough to do in bash.

```
#!/usr/bin/env bash

echo "Hello World"
```

How does this work? The first line is the "shebang". It indicates to the
shell how to execute this file. I use `/usr/bin/env bash` because one
can never never be certain where the bash executable lives on a given
system (maybe `/bin/bash`, or even `/usr/local/bin/bash`). I've never
had such a problem with `/usr/bin/env bash`. The following lines are
executable bash commands. The `echo` built in command prints text to
standard output. So save this file on your system as `hello-world`, then
`chmod +x hello-world`, and finally run `./hello-world`. Naturally your
computer will say hello to you.

Great, simple enough! Now let's parameterize this program so it can say
hello to a particular person. This quick exercise illustrates how bash
handles arguments. Bash programs (and functions) take any number of
arguments. Bash programs also do not explicitly declare their arguments.
Programs receive their arguments in numbered variables. These are also
referred to as "positional arguments". This is demonstrated below.

```bash
#!/usr/bin/env bash

echo "Hello $1"
```

Invoke this program by running `./hello-world bob`. Naturally you'll see
a nice greeting on the screen. The `$1` variable refers to the first
argument given on the command line. You may ask what about `$0`? That's
a great question! `$0` holds the name of the program itself (the first
item in the command line argument list). See what's happening? The
arguments passed are available as numbered variables. Running the program
with `./hello-world bob dylan` assigns `dylan` to `$2`. Now that we
understand argument passing, we can update the program to be
strict about its arguments. After all the program can't say hello
if doesn't know who to greet. Luckily for us bash has built in control
structures. Let's update the program to check that it's given an
argument and act accordingly.

```bash
#!/usr/bin/env bash

name="$1"

if [[ -z "${name}" ]]; then
  echo "USAGE: $0 NAME" 1>&2
  exit 1
fi

echo "Hello ${name}"
```

There are few things going on here. First, the `name` variable is
assigned using `=`. Next we see the awkward looking bash `if` control
structure. `if` evaluates to true if the given command exits 0. The
`[[ ]]` is a built command for evaluating different conditions. In
this case the `-z ARG` tests the given value is zero length (blank).
Bash requires `then` keyword followed by the code to execute. The `fi`
ends the `if` control structure. Inside the if block the usage
instructions are printed to stderr via output redirection (`1>&2`).
Next `exit` sets the exit status and terminates the process. Naturally
we exit non zero because the command failed. This program is not big
by any means but it mirrors structure for larger programs: declare
named variables, check arguments/options, then perform the task.
Patterns appear in all programming programs, this enables similar
problems to be solved in the same way.

## Elements of Style and Structure

I advocate applying best practices to problems of all sizes. This may be
a small demo script, but if one always applies best practices then this
will become second nature. Bash is no different. Best practices are
especially important because of the inherit quirks. The
[Google shell style guide][] is an
excellent starting point. It mentions style (things like quoting,
variable definitions, naming, etc) and structure. Together these two
things will keep on the happy path. This book makes some additions that
I've found useful in practice.

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
languages: blowing up on stupid mistakes and failures. Now with that out
the way we can get back to sanity.

[shellcheck][] is a godsend for Bash programmers. Bash
has many quirky behaviors that make it behave less like high level
languages. This is frustrating because it creates fiction and things may
break in weird or unexpected ways. Shellcheck solves 80% of the pain
points through static analysis. It picks up things like misspelled
variables, improper quoting, unused variables, uninitialized variables,
and much more. Shellcheck is as close as you are going to get to a
compiler for Bash programs. All the examples in this book pass
shellcheck on default settings from this point on.

Now for the next point: variable indicators. Bash allows you do many
things with variables which will be touched on later. We also saw that a
variable can be inserted (and interpolated) into a string anywhere.
However how does the interpreter know where a variable name begins and
ends? Bash generally does a very good job of making this transparent but
you may hit a problem. The correct way, is to use braces to indicate
variable names. This removes any confusion and makes it easy to use
parameter substitution (`${1:-}`) at any point in the program.

The next two points go together. Both are structural points and are
designed to ensure the program does not grow into a single chunk. Creating
functions is also a great way to ensure separation and make the program
more comprehensible.

Time to update the previous example so it fits our
elements of structure and style.

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

Let's unpack the example a bit. Defining functions is straight forward.
There are two functions: `usage` and `main`. The `main` function uses a
local variable `name` with `local` (according to the style guide). This
line also uses parameter substitution to insert a blank value for a
missing arguments. Using `set -u` requires this. This way running
`./hello-world` will not exit with an undefined variable error, but
print usage and exit. The if conditional now calls the `usage` function.
`return` replaces `exit`. This is important! `exit` will exit the
process which is not a problem when there are no functions. However,
functions should always use `return`. The program shouldn't exit because
a function completed right? Finally `main` is called on the last line.
`$@` is a special variable. It refers to all given arguments. Phew,
quite a bit of changes! However this structure is portable to programs
of all shapes and sizes. It will be second nature to you once you get in
the habit. It was actually hard for me to write the first example
because I was breaking my habit! Time to quickly go over what was
covered:

1. Declaring functions and handling arguments
2. Conditionals and empty value checking
3. Enabling sane defaults (unofficial "strict mode")
4. Proper structuring

This information has hopefully prepared you to enter the realm of
bash programming.

[google shell style guide]: https://google.github.io/styleguide/shell.xml
[shellcheck]: https://www.shellcheck.net/
