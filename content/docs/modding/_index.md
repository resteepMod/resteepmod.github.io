---
title: Make mods
weight: 40
bookFlatSection: true
---

# Making mods

ReSteep's goal is a real, usable modding API: mods that add content (models, textures, gear, maps), change gameplay
through the game's own systems, and talk to their own server half. Players switch mods on deliberately, and a server
can never push code to a player.

## What a mod can be

A mod is one folder (or a `.resteep` file of it) that may hold any mix of these parts:

| Part | What it does | Where it runs |
| --- | --- | --- |
| **In-game script** (`main.lua`) | Reacts to the rider (landings, crashes, sports), draws on screen, moves objects, changes the time and physics, has its own panel and windows | The player's game, in a Lua sandbox |
| **Content** (`resteep.json` → `content`) | New items and costumes, textures, texts, objects and whole new maps, challenges, music, animations | Built from the player's own install when the game starts |
| **Server script** (`mod.lua`) | Events, answers to the game's and the mod's own requests, leaderboards, admin tools | The server, in its Lua sandbox |
| **Native code** (DLLs) | Hooks on the game's code | Only after the player approved the exact files; never in shared mods |

Content mods carry only their own files. What they need from the game is generated on the player's PC, so nothing
of Ubisoft's is ever shipped in a mod.

## Where to go next

1. [Your first mod](first-mod.md): a working script mod in a few minutes.
2. [The mod format](format.md): `resteep.json`, `manifest.json` and the mod's files.
3. [The Lua API](lua-api.md): everything a script can call, and [a mod's own UI](ui.md).
4. [Content](content.md): items, costumes, maps, challenges, music and animations.
5. [Server mods](server-mods.md): the server half of a mod.
6. [Publishing](publishing.md): checking, packing and sharing a mod.

The [official mods](https://github.com/resteepMod/official-mods) are working examples of every kind: start from the
one closest to your idea.
