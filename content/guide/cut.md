---
title: "cut(1)"
author: "Adam Hawkins"
date: 2021-03-18T21:15:44-10:00
toc: true
tags:
  - shell
  - bash
---

> cut -- cut out selected portions of each line of a file

`cut` is a general purpose text splitter and extractor. It operates in
two modes. The `-d` sets the delimiter and `-f` specifies the "fields"
to exact. The `-c` option specifies the character positions to take.
`cut` is _really_ useable in day to day shell programming because you
can use to take semi structured data (such as a person's name) and
extract structured bits (such as the given or family name). `cut` has
one confounding quirk: Indexes start at 1 unlike most things in
programming. Here are some examples:

    $ echo "Adam Hawkins" | cut -d ' ' -f 1
    Adam
    $ echo "Adam Hawkins" | cut -c 1-4
    Adam
    $ echo "Adam Andrew Hawkins" | cut -d ' ' -f 1,2
    Adam Andrew

## Use Case

`cut` works perfectly for simple text manipulation and extraction like
pulling data from CSV files, TAB separated data, or semi structured
text. It's analogous to Ruby's `String#split` and array accessors like
`foo[1..3]`. It's easier than `awk` (and more readable) for simple
things. `cut` works with single character delimiters, so you cannot
use a regex or other more complex splitting criteria. Consider
extracting the path from a URI. Using `cut` here would be clunky
because paths themselves may contain `/` (the delimiter character).
`sed` or `grep` fit better in such cases because they support regular
expressions.

## Signature & Key Options

    cut -b list [-n] [file ...]
    cut -c list [file ...]
    cut -f list [-d delim] [-s] [file ...]

This usage synopsis comes from the BSD version because it identifies
the three different usage modes: bytes, characters, and delimiters.
Remember that `list` indexes **start at 1, not zero** (Cut apologizes
in advance for making you remember that).

- `-b` specifies byte `list` from `file`. Use this when you need to
  extract bytes from structured binary files (some TCP dump for
  instance). Combine with `-n` for multi-byte characters.
- `-c` select character `list` from `file`. Specify multiple ranges
  with `,`. Examples: take 5 characters - `-c 5`; take the first 3 and
  10-15; `-c 1-4,10-15`.
- `-f` selects `list` fields from `file` split by `-d`. `-d` defaults
  to `\t`. Specify multiple ranges with `,`. Examples: second word
  from a sentence -`echo "the quick brown fox" | cut -d ' ' -f `; take
  the first and third words - `echo "the quick brown fox" | cut -d ' ' -f 1,3`. `-d` only accept single character values. `-s` surpasses
  lines without delimiter. Use this when input files may contain junk
  data.

## GNU vs BSD

The BSD and GNU versions are similar functionality similar.

- The GNU version supports a `-z` or `--zero-terminated` useful when
  used with `find -print0` and `xargs -0`.
- The GNU version supports `--complement` to invert the match
  specified with `-b`, `-c`, and `-f`. This option is useful when you
  have many fields and want to print all but a few of them
