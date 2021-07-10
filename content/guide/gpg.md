---
title: "GPG (gnupg)"
author: "Adam Hawkins"
date: 2021-07-09T20:31:30-10:00
description: |
  Setup and use GPG for Git, SSH w/Yubikey
---

This guide is a tl;dr of this [fantastic guide][guide]. It's an
outline if you've already been through the process. Or you (if like
me) have been through this a few times and need a refresh course when
you need to setup a new device or rotate keys.

I decided to write this down after cocking this process up a few times
resulting in keys I couldn't use or new machines I couldn't set up.
The original guide is great but you can miss important details if you
skim it.

## Step One: Create Keys

These steps take place in a **pristine** `GNUPGHOME`. This is important
because you will need a complete copy of the keyring to prepare
multiple YubiKeys. Moving keys to a Yubikey is a destructive action,
so if you setup one key then need to setup another, then you will have
access to the necessary secret keys.

Also note that the master key **should not** expire. This will allow
you generate and rotate subkeys.

1. Create a fresh `GNUPGHOME` directory
2. Create a new GPG key that does not expire. Grant that key only
   `certify` capabilities
3. Add extra UIDs (i.e. emails)
4. Create `Sign`, `Encrypt`, and `Authorization` subkeys that do
   expire.
5. Export a revocation certificate to a secure backup
6. Export the set master and subkeys to a secure backup
7. Export the public key to a secure backup
8. Copy the `GNUPGHOME` directory to a secure backup

Check your work with `gpg -K` for secret keys and `gpg -k` for public
keys.

## Step Two: Setup Yubikey

If this is your first time configuring the Yubikey, then make sure you
note down the Admin PUK. You'll need that to move subkeys to the
Yubikey. You may need to do this again years in the future so it helps
to have it access.

0. Check your backup of `GNUGPHOME` from the previous step
1. Copy that new a new temporary `GNUGPHOME`
2. Move all sub keys to the Yubikey

Check your work with `gpg --card-status`

## Step Three: Setup Your Workstation

At this point you have everything you need to configure real world
use. The Yubikey has the subkeys used for signing, encryption, and
authentication. The backup contains the public key required to use the
Yubikey.

0. Start a new shell outside the `GNUPGHOME` of any the previous steps
1. `gpg --import` the public key from step one

Check your work with `gpg -K`. You should see the secret keys nows.

Now continue to follow the [guide][] for:

- Configuring the GPG agent and pinentry to actually use this
- SSH + GPG agent for SSH
- git commit signing

See my [dotfiles][] for examples.

## Endnotes

- Sign your commits because they're special. Take pride in your work.
- `scdaemon.confg` may need `disable-ccid`. I did not need this but
  something changed that caused me to add it.
- If you forget the Yuikey PINs, then you use the admin tools to rest
  them and wipe all the keys. Importantly this **does not** reset
  anything like (like TOPT generators).
- MacOS: Use `pinentry-mac`
- MacOS: do not use the "GPG tools" packages; just use `gnupg` from
  `brew`

[guide]: https://github.com/drduh/YubiKey-Guide
[dotfiles]: https://github.com/ahawkins/dotfiles
