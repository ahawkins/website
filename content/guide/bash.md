---
title: "Bash"
author: "Adam Hawkins"
date: 2021-03-18T21:00:04-10:00
tags:
  - shell
  - bash
---

Bash is a powerful tool. It may glue systems together. It may glue
workflows together. It can close gaps in workflows. It exposes the
power of the command line to any workflow. It's the force. Master it
and you will move mountains.

## Command Guides

- [xargs][]: The One Liner Chainsaw!
- [cut][]: Like `split` in many programming languages
- [find][]: Search for files or directories
- [comm][]: Set logic (and, or, intersect)

## My Standard Lib

What follows is my own standard library of useful Bash functions.
They're handy when writing scripts. Copy and use at will. The `log::*`
functions are especially handy for providing transparency to users.
Output is nicely colored too.

{{< gist "ahawkins" "694a02768641d7850d0b4b21e2c93b91" >}}

[xargs]: {{< ref "guide/xargs" >}}
[cut]: {{< ref "guide/cut" >}}
[find]: {{< ref "guide/find" >}}
[comm]: {{< ref "guide/comm" >}}
