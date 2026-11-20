---
title: Mod safety
weight: 30
---

# Mod safety

## What a mod can do

Most mods are **data** (gear, textures, texts, world edits) and **Lua scripts**. The scripts run in a sandbox: they
use what ReSteep's mod interface offers, but can't open your other files, start programs or reach the internet. Each
mod has its own memory and time budget; a mod that errors or runs too long is stopped, and the others go on.

## Checks at install

ReSteep checks every mod file before it installs it, and **nothing in a mod runs while it is installed**. Mod files
are unpacked with strict rules: no paths outside the mod, no links, size limits against zip bombs. A mod with errors
is listed with them, but never built or loaded.

A mod is refused when it contains programs or scripts that would run outside the Lua sandbox (`.dll`, `.exe`, `.ps1`,
`.bat`, `.sh`, `.py`, ...), or when it would unlock the game's paid content for players who don't own it.

## Native code

A few mods carry **native code** (DLL files). Native code can do anything your user account can, like any program you
run. So ReSteep never loads it on its own:

- You have to **approve** it, and the approval is **pinned to the exact files** (their SHA-256 hashes). Any change
  asks again.
- **A server can never send code to your game or approve it for you.**
- Native code is never part of shared mod listings: you add such a mod by hand.

How you approve it today:

- **Windows:** the installed ReSteep doesn't load a mod's native code yet. From the source code,
  `python -m resteep approve <mod id>` shows each file with its size and hash; `revoke` takes the approval back.
- **Linux:** a mod with native code is a folder you put into `mods/` yourself. Switching it on is your approval.

> [!CAUTION]
> Approve native code only from people you trust.

## Mods on a server

A server tells you which mods it runs, but never installs anything on your PC. Server-side Lua mods run in the
server's own sandbox, chosen by the host.
