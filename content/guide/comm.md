---
title: "comm(1)"
author: "Adam Hawkins"
date: 2021-03-18T21:27:24-10:00
tags:
  - shell
  - bash
---

> comm -- select or reject lines common to two files

`comm` takes two files as input. It prints three columns: Lines only
in file 1; Lines only in file 2; lines in both files. This is
effectively set logic (picture a Venn diagram). Here's some examples:

    $ cat > colors1.txt <<-EOF
    blue
    green
    red
    yellow
    EOF
    $ cat > colors2.txt <<-EOF
    green
    orange
    yellow
    EOF
    # Print items only in colors1.txt
    $ comm -23 colors1.txt colors2.txt
    blue
    red
    # Print items only in colors2.txt
    $ comm -13 colors1.txt colors2.txt
    orange
    # Print items in both files
    $ comm -12 colors1.txt colors2.txt
    green
    yellow
    # Print all colums at once
    $ comm colors1.txt colors2.txt
    blue
        green
      orange
    red
        yellow

The last example has the strangest output due to how `comm` prints
multiple columns. The `-1`, `-2`, and `-3` options suppress the
relevant columns for easier consumption.

`comm` requires that files are sorted and do not contain duplicate
items. Thus, this style invocation is common: `comm -23 <(sort -u file1.txt) <(sort -u file2.txt)`. The `<()` writes the output of the
command (`sort -u`, `-u` means unique items only) to temporary file
and returns the temporary file. This is a great workaround for `comm`
because input files may not meet requirements.

The `-i` uses case insensitive comparison.

## Recap

This guide is shorter than the others because there's not too much
to show. Here are some use cases to help crystalize it it:

- Set subtraction and intersection (and'ing)
- Given two files containing list of files; use `comm` to determine
  which files to keep or delete

Options are easy as well:

- `-1` Suppress the first column (items only in file 1)
- `-2` suppress the second column (items only in file 2)
- `-3` suppress the third column (items on both files)
- `-i` case insensitive comparison
