---
title: "Bash Bootcamp: Writing Usage Descriptions"
author: "Adam Hawkins"
date: 2021-06-04T22:39:56-10:00
tags:
  - shell
  - bash
summary: |
  How to write usage descriptions for help output and man pages
---

We have all seen these. The examples have included them. They're in
every man page. But what's expected to be in a usage description? How
they describe optional vs required flags? What about required positional
arguments? What about indefinite argument lists? There is a generally
agreed upon standard for how to communicate these things. Let's dive in
so the documentation for our programs matches user's expectations.

Consider this excert from `sed` man page. It demonstrates almost
everything.

```
sed [-Ealn] command [file ...]
```

Optional arguments are wrapped in `[ ]`. This usage description tells us
that the `-E`, `-a`, `-l`, and `-n` flags are optional. Required
positionl arguments are written as is. You may see these in all caps.
This is really the author's preference. Next there is an optional
indefinite list of files. This denoted by `[ ]` and using `...` to
represent any number of files may be provided. This mostly used with
shell globging. Here are some example invocations.

    $ cat words.txt | sed s/hi/HI/g
    $ sed s/hi/HI/g chapter1.txt chapter2.txt
    $ set s/hi/HI/g chapter*.txt

The first example does not provide any `file` arguments. Instead output
it piped to `sed`. This is why `file` is optional. However it's not
possible express conditional logic in usage description. This is why
complete documentation is so important. Let's continue our exploration
by looking at the `grep` man page.

```
grep [-abcdDEFGHhIiJLlmnOopqRSsUVvwxZ] [-A num] [-B num] [-C[num]]
		 [-e pattern] [-f file] [--binary-files=value] [--color[=when]] [--colour[=when]]
		 [--context[=num]] [--label] [--line-buffered] [--null] [pattern] [file ...]
```

This is a long one! Let's skip over the bits we've already covered.
`grep` takes option arguments as well. There is an optional `-A` option
argument. It's also best practice to give the value a meaningful name in
the. `[-A num]` tells the reader that `-A` is optional and takes a
numeric argument. `num` is never actually used in the program, it's
purely for the reader. Continuing on we see that `grep` mixes long and
short options. The usage states grep uses the `--foo=bar` long option
form. There is an optional `--binary-files` option which requires a
`value`. Thus `--binary-files=true` is valid, but `--binary-files` or
`--binary-files=` are invalid forms. Next there is `[--color[=when]]`.
Curious! Nested brackets. This means the `--color` optional optionally
accepts a value. So `--color` and `--color=matched`. are valid forms.
One must read the man page to see what the accepted `when` values are.

We've covered optional options but what about required options?
Consider this example.

```
vagrant-workstation up -n NAME -v VAGRANTFILE -p PROJECT_PATH
```

There are three required option arguments: `-n`, `-v`, and `-p`. The
values are given descriptive names to inform the header. Lastly is one
more important thing to cover. We saw previously that `--` indicates the
end of options. Anything after `--` should be ignored by the invoking
program. This is commonly used for programs that invoke other programs
where arguments can be passed. Consider this description.

```
npm run PROGRAM [-- PROGRAM_OPTIONS ...]
```

This indicates there is a required `PROGRAM` argument. Next is an
optional indefinite list of `PROGRAM_OPTIONS` indicated by `[ ]` and
`...`.
