---
title: Publishing
weight: 70
---

# Checking, packing and sharing a mod

The ReSteep repository has a command line for mods (`python -m resteep ...`, from a checkout):

```
python -m resteep new my-mod                 a new script mod (--slot=hats: an item; --kind=costume / map)
python -m resteep check mods/my-mod          errors and warnings, as the launcher sees them
python -m resteep pack mods/my-mod           -> my-mod-1.0.0.resteep
python -m resteep pack mods/my-mod --zip     -> my-mod-1.0.0.zip, Thunderstore's upload
python -m resteep pack mods/my-mod --tcli    -> a project for Thunderstore's CLI
python -m resteep list                       what is in the mods folder, with problems and dependencies
python -m resteep convert mods/old-mod       an older layout (BlueBird, Powder) into the new one
```

Packing the same files always gives the same bytes.

## Sharing

Upload the `.resteep` file anywhere. Players add it on the launcher's **Mods** page or drop it into their mods folder.

**Thunderstore:** the `--zip` file is Thunderstore's own package layout. A Steep community on thunderstore.io has been
requested and doesn't exist yet; until it does, sharing works through `.resteep` files. Once it does, the launcher's
**Thunderstore** tab lists its mods.

**Official mods:** the team's mods live in [resteepMod/official-mods](https://github.com/resteepMod/official-mods).
After a change, bump the mod's version and rebuild the index (`python -m resteep index ../official-mods`) so the
launcher offers the update.

## The ReSteep version a mod needs

Say it once, in `resteep.json`: `"resteep": "0.1"`. For Thunderstore and mod managers, `pack` writes the same as a
dependency on the base package `ReSteep-ReSteep-X.Y.Z`. A mod made for a newer ReSteep than the one running loads
with a warning.

## What a shared mod may contain

A shared package holds **data and sandboxed Lua only**. `pack` and installing refuse programs and scripts (`.dll`,
`.exe`, `.ps1`, `.bat`, `.cmd`, `.sh`, `.py`, `.js`, `.jar`, ..., or a program under any name). A mod folder with them
still works when a player adds it by hand, and `check` warns that it can't be published.

Before you share, read the [rules for shared mods](../about/rules.md#rules-for-sharing-mods):

1. No mods that unlock paid content.
2. No executables or scripts outside the Lua sandbox.
3. No game files, or data taken from the game.

> [!TIP]
> Keep the mod's `id` and its items' `key`s the same across versions: they decide where settings are stored and the
> items' ids, which players' saves refer to.
