---
title: "Bash Bootcamp: Argument Parsing"
author: "Adam Hawkins"
date: 2021-06-04T22:39:56-10:00
tags:
  - shell
  - bash
summary: |
  Parsing short and long option formats
toc: true
---

All programs need to collect input from. CLI programs usually collect
their arguments from command line itself (yes, environment variables and
configuration files can be used as well). You've seen things like `make -B`, or `grep --verbose`, and `echo foo`. All of these are given
arguments demonstrate a different type. First there are single switches.
These are prefixed with a single `-` and may be combined. This means
`grep -Q -F` is the same as `grep -QF` or `grep -FQ`. They may also be
combined with a value like `foo -x bar`. In this case the `-x` option is
to `bar`. Next up are GNU style long options. These are usually the
easiest to remember because they are a complete word. They come in a few
flavors. There is the `foo --bar`, `foo --bar=baz`, or `foo --bar baz`.
The first examples sets `--bar`. The next set `--bar` to `baz`. The
third example is a named argument. Usually most CLI programs accept a
mix of all three. This section covers how to translate command line
arguments into settings for your program.

## Short Options

Short options are most straight forward way to handle option flags
because the `getopts` command is built into the shell. It provides
handling for:

- Valueless options (`-v`)
- Options with value (`-d bar`)
- Combining options (`-xyz`)
- Handling unknown options
- Handling missing values for option values

Let's write small program demonstrating each case. Many programs have
a verbose/debug option. The program should produce more output than usual
option is set. This example also demonstrates how to set the default
value.

```bash
#!/usr/bin/env bash

set -euo pipefail

main() {
  local verbose="" # 1

  while getopts ":v" opt; do
    case "${opt}" in
    v)
      verbose=true # 2
      ;;
    esac
  done

  shift $((OPTIND - 1)) # 3

  if [[ -n "${verbose}" ]]; then # 4
    echo "Some more detailed information!"
  fi

  echo "Nothing to say here"
}

main "$@"
```

1. Initialize `verbose` as an empty variable. This avoid failures
   caused by `set -u`.
2. Assign an non empty value. Bash does not have boolean values, so
   this is the next best thing.
3. `OPTIND` is the index in the argument list `getopts` read up to.
   `shift` removes all the entries in the argument list that where
   parsed with `getopts`. More on this later.
4. The `-n` test flag is short "non zero length string".

Assume this file is named `short-options`. Running `short-options`
should process a single output line

```
$ ./short-options
Nothing to say here
```

Now pass `-v`

```
$ ./short-options -v
Some more detailed information!
Nothing to say here
```

All this is pretty straight foward. Time to turn a bit malicious. What
happens if we provide options that don't exist? Let's see what happens.

```
$ ./short-options -x
Some more detailed information!
Nothing to say here
```

This doesn't seem right does it? Programs usually present some usage or
help style message when given an unknown argument or option. This is
easy to handle in our `getopts` form. We need to handle the unknown
case.

```bash
#!/usr/bin/env bash

set -euo pipefail

main() {
  local verbose=""

  while getopts ":v" opt; do
    case "${opt}" in
    v)
      verbose=true
      ;;
    *)                                       # 1
      echo "Unknown option: -${OPTARG}" 1>&2 # 2
      return 1
      ;;
    esac
  done

  shift $((OPTIND - 1))

  if [[ -n "${verbose}" ]]; then
    echo "Some more detailed information!"
  fi

  echo "Nothing to say here"
}

main "$@"
```

1. `*` express the default or "catch all case". Here we print an error
   and return.
2. `getopts` automatically sets the `OPTARG` value. It refers to the
   currently matched option.

Invoke this program and see what happens:

```
$ ./short-options -f
Unknown option -f
```

Now we've covered how to use `getopts` for basic options. Time to move
onto option arguments. Option arguments are options with values.
Consider the this commmand: `usermod -a -G docker ahawkins`. You may
have come across this before. There are two different things in play.
There is the `-a` option which has no value. Second there is the `-g`
option argument which has value `docker`. `getopts` supports this form
by modifying the format string. The `getopts` string for this form is
`:ag:`. Values with `:` after them require an argument. Let's update the
example to take `-n VALUE`.

```bash
#!/usr/bin/env bash

set -euo pipefail

main() {
  local verbose=""
  local name="Anonymous"

  while getopts ":vn:" opt; do
    case "${opt}" in
    v)
      verbose=true
      ;;
    n)
      name="${OPTARG}" # 1
      ;;
    :) # 2
      echo "Value missing for -${OPTARG}" 1>&2
      return 1
      ;;
    *)
      echo "Unknown option: -${OPTARG}" 1>&2
      return 1
      ;;
    esac
  done

  shift $((OPTIND - 1))

  if [[ -n "${verbose}" ]]; then
    echo "Some more detailed information!"
  fi

  echo "Nothing to say here"
  echo
  echo "- ${name}"
}

main "$@"
```

1. `OPTARG` takes a different value here. `OPTARG` holds the value
   when the option value requires a value.
2. `:` is a special value used by `getopts`. It expresses the option
   was known but a value was not given. It's used here to present the
   user with a useful error message.

We've covered how to handle all possible cases with `getopts`. It's time
to talk about `OPTIND` and the argument list. Let's rewrite the hello
world program from the previous chapter to match this signature:
`greet [-h] NAME`. The program prints a gretting for the specified
`NAME`. Setting `-h` will print a happier greeting. I'll ommit the
`OPTIND` bit to demonstrate its importance.

```bash
#!/usr/bin/env bash

set -euo pipefail

usage() {
  echo "${0} [-h] NAME"
}

main() {
  local happy=""

  while getopts ":h:" opt; do
    case "${opt}" in
    h)
      happy=true
      ;;
    *)
      echo "Unknown option: -${OPTARG}" 1>&2
      usage 1>&2
      return 1
      ;;
    esac
  done

  if [[ -n "${1:-}" ]]; then
    usage 1>&2
    return 1
  fi

  if [[ -n "${happy}" ]]; then
    echo "Whoa!! What's up ${1}?"
  else
    echo "Hey ${1}?"
  fi
}

main "$@"
```

Let's run he program. First give it a single argument. Things work as
expected.

```
$ ./greet John
Hey John
```

Now try to get a happy greeting.

```
$ ./greet -h John
Whoa!! What's up -h?
```

Well this is a bit strange right? `-h` is not the name argument, that
should be `john`. This is definitely not the desired behavior. So what's
happening? First we must understand how the `while getopts` loop is
working. This is walking each item in the argument list. Running `greet -h john` creates an argument list with two items: `-h`, and `john`.
`getopts` sees the first argument as `-h`. It knows that this is an
option and should be handled accordingly. Then it processes `john` next.
This argument does not look like an option (it does not start with -) so
`getopts` returns non zero and while loop ends. `OPTIND` holds the index
for how far `getopts` read in the argument list. Given these items are
options flags we most likely do not care about them anymore. This is
where `shift` comes in. `shift` removes a given number (defaults to `1`)
from the argument list. Note that calling shift changes the value for
positional argument variables (`$1`, `$2`, etc). So it's important to
understand that these variables are not constant. Instead they can be
manipulated at runtime by calling `shfit`. How does this all relate to
the original problem? Well, the program uses `$1`, but it contains `-h`.
The solution is to just chop of everything `getopts` parsed from the
argument list. This does require you as the program author to decide the
order of positional arguments and option flags.footnote:[options
order,Accepting options before positional arguments is the agreed upon
best practice. You should follow this guideline. This is why the
examples are done in this way.] Here's the correct source code.

```bash
#!/usr/bin/env bash

set -euo pipefail

usage() {
  echo "${0} [-h] NAME"
}

main() {
  local happy=""

  while getopts ":h:" opt; do
    case "${opt}" in
    h)
      happy=true
      ;;
    *)
      echo "Unknown option: -${OPTARG}" 1>&2
      usage 1>&2
      return 1
      ;;
    esac
  done

  shift $((OPTIND - 1)) # 1

  if [[ -n "${1:-}" ]]; then
    usage 1>&2
    return 1
  fi

  if [[ -n "${happy}" ]]; then
    echo "Whoa!! What's up ${1}?"
  else
    echo "Hey ${1}?"
  fi
}

main "$@"
```

1. `$(( ))` is used for arthmetic. Bash can handle simple expressions.
   Variables do need the `$` prefix in arthmetic expressions.

That covers everything you need to know when it comes to handling short
options. Let's quickly review the common structure for short option
parsing.

```bash
# getopts format strings should start with :. Then list all options that
# do not require a value. Next list options that do require a value each
# followed by :. This example assumes -v has no value, and -a does have
# a value.
while getopts ":fa:" opt; do
  case "${opt}" in
  f)
    # Logic for -v flag
    ;;
  a)
    # Logic for -a flag. Use $OPTARG for value.
    ;;
  :)
    # Logic for when value required, but none provided.
    # Use $OPTARG for option in question.
    ;;
  *)
    # Logic for an uknown option.
    # Use $OPTARG for option in question.
    ;;
  esac
done

shift $((OPTIND - 1))
```

That concludes our jounery into short option parsing. This only covers
have the story. I'm sure you've seen programs that use arguments like
`--verbose` or `--no-atime`. What are these? They are definitely not
short options. They are long options.

## Long Options

GNU style long options are a nice way to make options more memorable.
You will recognize them in three forms: `--verbose` for simple option
flags. Then `--log-file foo.log` or `--log-file=foo.log` for options
with values. Unfortunately there is no built in function like `getopts`
to handle long options. Parsing long options is by looping over the
argument lists and handling each one in turn and shifting off what's
been parsed. Let's refactor the previous it to use long options starting
with the happy path. We'll add error handling and other important bits
as we go.

```bash
#!/usr/bin/env bash

set -euo pipefail

usage() {
  echo "USAGE: ${0} [--happy] NAME"
}

main() {
  local happy=""

  for arg in "$@"; do
    case "${arg}" in
    --happy)
      happy=true
      shift
      ;;
    esac
  done

  if [[ -z "${1:-}" ]]; then
    usage 1>&2
    return 1
  fi

  if [[ -n "${happy}" ]]; then
    echo "Whoa!! What's up ${1}?"
  else
    echo "Hey ${1}"
  fi
}

main "$@"
```

This programs behaves in the following ways:

1. Fails and prints usage when no arguments are given
2. Fails and prints usage when only `--happy` given
3. Prints happy greeting when `--happy` is given
4. Prints a standard greeting when `--happy` is not given.

Let's try it out.

```
$ ./greet-long
USAGE: greet-long [--happy] NAME
```

```
$ ./greet-long --happy
USAGE: greet-long [--happy] NAME
```

```
$ ./greet-long ahawkins
Hey ahawkins
```

```
$ ./greet-long --happy ahawkins
Whoa!! What's up ahawkins?
```

Let's make the program more strict. The program should also print usage
when an unknown option (e.g. `--junk`) is given. This is done by
updating the `case` statement inside the for loop to match arguments
that look like long options but have not hit any prior case.

```bash
#!/usr/bin/env bash

set -euo pipefail

usage() {
  echo "USAGE: ${0} [--happy] NAME"
}

main() {
  local happy=""

  for arg in "$@"; do
    case "${arg}" in
    --happy)
      happy=true
      shift
      ;;
    --*)
      echo "Unknown option ${arg}" 1>&2
      usage 1>&2
      return 1
      ;;
    esac
  done

  if [[ -z "${1:-}" ]]; then
    usage 1>&2
    return 1
  fi

  if [[ -n "${happy}" ]]; then
    echo "Whoa!! What's up ${1}?"
  else
    echo "Hey ${1}"
  fi
}

main "$@"
```

Now run the program with `--junk` and see what happens.

```
$ ./greet-long --junk
Unknown option --junk
USAGE: greet-long [--happy] NAME
```

```
$ ./greet-long --junk ahawkins
Unknown option --junk
USAGE: greet-long [--happy] NAME
```

This covers an unknown long option but what about an unknown short
option? Let's run the program with `-j` and see what happens.

```
$ ./greet-long -j
Hey -j
```

Well, schucks! This is not what we want. Our program expects only long
options. Catching this case is an easy change to the program. Let's
update the lastest `case` statement to match anything that looks like an
option. That means any argument starting with `-`.

```bash
#!/usr/bin/env bash

set -euo pipefail

usage() {
  echo "USAGE: ${0} [--happy] NAME"
}

main() {
  local happy=""

  for arg in "$@"; do
    case "${arg}" in
    --happy)
      happy=true
      shift
      ;;
    -*)
      echo "Unknown option ${arg}" 1>&2
      usage 1>&2
      return 1
      ;;
    esac
  done

  if [[ -z "${1:-}" ]]; then
    usage 1>&2
    return 1
  fi

  if [[ -n "${happy}" ]]; then
    echo "Whoa!! What's up ${1}?"
  else
    echo "Hey ${1}"
  fi
}

main "$@"
```

Let's see how the program handles junk input now.

```
$ ./greet-long --junk
Unknown option --junk
USAGE: greet-long [--happy] NAME
```

```
$ ./greet-long -j ahawkins
Unknown option -j
USAGE: greet-long [--happy] NAME
```

Great! The program correctly handles all the edge cases for valid and
invalid options. This covers the first of three forms mentioned at the
beginning of this section. Now it is time to tackle the `--foo=bar` and
`--foo bar` forms. Let's add a `--day` option value. The program will
optionally include the provide value in the greeting. The `--day bar`
form is more straight forward because value is next item in the argument
list. This also requires the program validate that _is_ a next item in
the argument list. The second form require some messaging. When
`--day=*` matches, then extract everything after the `=` and assign to a
variable. The program must handle the case where there is nothing after
the `=`. Let's tackle all these cases at once.

```bash
#!/usr/bin/env bash

set -euo pipefail

usage() {
  echo "USAGE: ${0} [--happy] [--day DAY] NAME"
}

main() {
  local happy="" day=

  for arg in "$@"; do
    case "${arg}" in
    --happy)
      happy=true
      shift
      ;;
    --day) # 1
      if [[ -n "${2:-}" ]]; then
        day="${2}"
        shift 2
      else
        echo "--day requires a value" 1>&2
        usage 1>&2
        return 1
      fi
      ;;
    --day=?*)         # 2
      day="${arg#*=}" # 3
      shift
      ;;
    --day=) # 4
      echo "--day requires a value" 1>&2
      usage 1>&2
      return 1
      ;;
    -*)
      echo "Unknown option ${arg}" 1>&2
      usage 1>&2
      return 1
      ;;
    esac
  done

  if [[ -z "${1:-}" ]]; then
    usage 1>&2
    return 1
  fi

  if [[ -n "${happy}" ]]; then
    echo "Whoa!! What's up ${1}?"
  else
    echo "Hey ${1}"
  fi

  if [[ -n "${day}" ]]; then
    echo "Heads up! It's ${day}"
  fi
}

main "$@"
```

1. This form is handled with direct equality.
2. This is not a regex. This is a [pattern][bash pattern]. `?` means any
   single character. The `*` matches zero or more of any character.
3. This <<parameter-substitution>>. You've already seen it before with
   `${1:-}`. This form returns everything after the `=`. Parameter
   substitution is a big topic in Bash. There will be much more on
   that later.
4. This case must be listed after the previous case.

The program now handles all the failure and happy scenarios along with
the two different long option forms. Not bad right? It requires a bit
more hoops to jump through but the end result is a bit more user
friendly.

## Mixing Long and Short Options

You may be thinking, wouldn't it possible to accept both long
and short options? Yup, we sure can. Just change the case statements
appropriately. Let's update the program to accept `-h` for `--happy` and
`-d FOO` for `--day FOO`.

```bash
#!/usr/bin/env bash

set -euo pipefail

usage() {
  echo "USAGE: ${0} [--happy] [--day DAY] NAME"
}

main() {
  local happy="" day=

  for arg in "$@"; do
    case "${arg}" in
    --happy | -h) # 1
      happy=true
      shift
      ;;
    --day | -d) # 2
      if [[ -n "${2:-}" ]]; then
        day="${2}"
        shift 2
      else
        echo "--day requires a value" 1>&2
        usage 1>&2
        return 1
      fi
      ;;
    --day=?*)
      day="${arg#*=}"
      shift
      ;;
    --day=)
      echo "--day requires a value" 1>&2
      usage 1>&2
      return 1
      ;;
    -*)
      echo "Unknown option ${arg}" 1>&2
      usage 1>&2
      return 1
      ;;
    esac
  done

  if [[ -z "${1:-}" ]]; then
    usage 1>&2
    return 1
  fi

  if [[ -n "${happy}" ]]; then
    echo "Whoa!! What's up ${1}?"
  else
    echo "Hey ${1}"
  fi

  if [[ -n "${day}" ]]; then
    echo "Heads up! It's ${day}"
  fi
}

main "$@"
```

1. `|` matches this or that. So simply provide the literal optional
   flag.
2. `|` matches this or that. So simply provide the literal optional
   flag.

That surprisingly easy! This wraps up the section on long options.

## Conclusion

This chapter has covered all the ways to get option flags into your
program. We've covered using the built in `getopts` function to parse
short options. Next we we implemented long options with a loop. We've
made our programs robust enough to handle the following scenarios in
each case:

1. Unknown option
2. Option argument missing a value
3. Options with required arguments
4. Option flags

Finally we dicussed how to document a programs options and arguments in
proper usage description. Doing all these things introduced a few
concepts:

- loops
- case statement for handling options
- `shift` to manipulate the argument list
- Using `--` to indicate end of options
- [parameter substitution][] for working with variables

[style guide]: https://google.github.io/styleguide/shell.xml
[shellcheck]: https://www.shellcheck.net/
[parameter substitution]: https://tldp.org/LDP/abs/html/parameter-substitution.html
[bash pattern]: https://wiki.bash-hackers.org/syntax/pattern
