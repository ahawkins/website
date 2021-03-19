---
title: "find(1)"
author: "Adam Hawkins"
date: 2021-03-18T21:19:35-10:00
---

`find` is a general purpose file/directory search tool. It combines
various filters (such as comparing by modified time, executable files,
types, and more) along with command execution. Create powerful
pipelines by combining `find` with other commands. Here are some
common examples:

    # Recursively find all directories in the current directory
    $ find . -type d
    # Recursively find all files in the current directory
    $ find . -type f
    # Pipe find to xargs
    $ find . -type -f -print0 | xargs -0

`find` is a powerful command with many options and features via
expressions. Expressions include tests, actions, global options,
positional arguments, and operators. Tests return true/false. Actions
have side effects. Global options apply to everything in an
expression. Positional options only affect tests or actions which
follow them. Operators join other items in expressions.

Let's unpack the examples.

`find . -type d` uses the `-type` test. `-type` returns true if the
file matches the given type. Common types are `d` for directory, `f`
for file, or `l` for symbolic links. `find` assume the `-print` action
when nothing is provided. The second example uses `-type f` to print
all files. The third example uses the `-print0` action. This prints
null terminated output for use combinations with `xargs -0`. These
options make `find` and `xargs` place nice when files names include
delimiting characters (such as whitespace).

Naturally there are more tests than just `-type`. Let's cover the use
cases before diving deeper into expressions and examples.

## Use Case

`find` is a general purpose file and directory search. It is useful in
shell programs with conditional logic (e.g. match this _or_ that) or
to recursively find everything in a set of directories. Generally `ls`
is used for simple directory listings, while `find` is for searching
and some form of batch processing.

## Key Options

- `-type`
- `-exec`, `-execdir`, `-ok`, `-okdir`
- `-print0`
- `-a`/`-and`, `-o`/`-or`
- `-name`, `-iname`
- `-path`, `-ipath`, `-regex`, `-iregex`
- `-E`
- `-L`
- `-size`
- `-delete`

## BSD vs GNU

Here's a summary of important differences between the GNU and BSD
versions. This is not exhaustive, instead it is optimized for things
you may encounter in day-to-day use. Refer to the [BSD find
manual](http://www.unix.com/man-page/FreeBSD/1/find/) and [GNU find
manual](http://man7.org/linux/man-pages/man1/find.1.html) for complete
information.

- BSD `find` supports the `-depth N` option. Both versions support
  `-depth` without a value. This triggers depth first traversal in
  both cases. BSD `-depth N` test if the file/directory is depth `N`
  from the initial traversal point. GNU `find` does not support
  `-depth N`.
- GNU `find` includes `-executable`, `-readable`, and `-writable`
  tests. BSD `find` uses `-perm` for similar functionality. GNU `find`
  effectively has shorthands for these common permissions.
- BSD `find` supports `-flags`, with both BSD and GNU find support
  `-perm`. `-perm` test permissions (read/write/execute). `-flags`
  maps to BSD specific file system flags. Refer to the (Free)BSD
  [chflags](http://www.unix.com/man-page/freebsd/1/chflags/) manual
  for more information.
- BSD `find` supports the `-X` option to skip files names with
  delimiting characters. This option intends to make `find` work
  correctly with `xargs` (which would break normally). Both BSD and
  GNU find support `-print0` which makes _all_ files play nicely with
  `xargs -0`.
- Both versions support `-E` for extended regex support. However the
  exact regex syntax varies between BSD and GNU.
- GNU `find` uses `-O LEVEL` for query optimizations. BSD `find` has
  no such option. Refer to the [GNU find
  manual](https://linux.die.net/man/1/find) for more information.
- BSD `find -s` cause find to traverse the file hierarchies in
  lexicographical order, i.e., alphabetical order within each
  directory. Note that `find -s` and `find | sort` may give different
  results. GNU `find` has no such option.
- GNU `find -D OPTS` manages debug options. Refer the [GNU find
  manual](http://man7.org/linux/man-pages/man1/find.1.html) for more
  information. BSD `find` has no such option.
- Both BSD and GNU `find` includes compatible options to skip files
  that are on different file systems than the original traversal
  point. Both versions implement `-mount`, while BSD `find`, uses a
  global `-x` option in favor of a depcreated `-xdev` option. GNU
  `find` does not support the `-x` option, but does support `-xdev`.
- GNU `find` supports the `-printf` action for formatting output. BSD
  `find` includes no similar feature.
- BSD "primaries" refer to GNU tests, actions, global options, and
  positional options.
