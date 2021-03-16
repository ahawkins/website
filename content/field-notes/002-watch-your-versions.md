---
title: Watch Your Versions
date: 2021-03-08T23:08:11-10:00
draft: true
---

Today I tried to add [Husy]({{< ref "handbook/husky" >}}) to this
project. I went through my standard workflow of `yarn add -D husky`
then declaring hooks in `package.json`. Then I tried to commit. Hook's
didn't work.

Why? It turns out that [Husky recently released version 5][husky5] which has an
entirely different workflow than version 4. Version 5 also mentioned a
yarn v1 vs yarn v2 install. There are different methods for installing
depending on Yarn version. Well that's interesting. Yarn version 2.
When did that come out? I know I'm on version 1 but figure I'll
checkout version 2 since it's news to me.

Well [Yarn V2 is a major release][yarn2] with many backwards
incompatible changes. The biggest being that installing through
something like `brew` is no longer supported. Yarn V2 is installed
with `npm install -g yarn`. Then you run `yarn config set version
berry` (yes that's "berry", a code name for the recent release). At
this point you can run `rm -rf node_modules` and try `yarn install`.
Next you need to add a bunch of `.yarn` files to `.gitignore` because
Yarn writes more files to `.yarn/`. Anyway it seems that version 2 is
a major release with significant backwards incompatible changes.

Those changes seem fine for the projects I tend to work on. So I
upgraded to v2 for this project just to start riding the latest
release. Riding the latest release is an important practice in low
risk environments. Which brings me back to Husky.

This small endevour revealed that two of my important tools have major
releases with breaking changes.

There's no way around this in software. No versions are released. Its
our job as software professionals to keep abreast of these
developments so we don't step into it when we least expect.

This is one case for the concept of auto-updating builds, meaning CI
should upgrade everything and see if the build passes. If the build
passes then the changes may be merged in. With this approach upgrades
are always happening. In other words, it's automated so it happens an
on an on-going basis. If it's not automated then it's left to us
humans. We tend to forget about updates, so as a result, the batch
size to update gets larger and complex, which in turn makes it less
likely to complete.

Anyways, It's **never** safe to assume that installing the latest
version of a library or tool will work as the last one (duh, right?).
I've been bitten by this recently with Husky just today and `yq` a few
weeks ago. Yq version 4 is completely different and no way compatible
with `yq` version 3. So that's what I get for relying on `brew`.
Thankfully there was an ASDF plugin for YQ so I could lock relevant
projects to version 3.

[husky5]: https://dev.to/typicode/what-s-new-in-husky-5-32g5
[yarn2]: https://dev.to/arcanis/introducing-yarn-2-4eh1
