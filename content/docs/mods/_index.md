---
title: Mods
weight: 30
bookFlatSection: true
---

# Mods

Mods add new gear, change textures and texts, add objects, places and whole new maps, add challenges and music, or
change how the game plays. This section is for players. To make mods, see [Make mods](../modding/).

## Install a mod

{{< tabs >}}
{{% tab "From the launcher" %}}
Open ReSteep's **Mods** page:

- **Official** lists the ReSteep team's mods ([resteepMod/official-mods](https://github.com/resteepMod/official-mods)):
  examples and content.
- **Thunderstore** lists the community's mods, once Steep has a community there.

**Install** downloads a mod and the mods it needs, and checks it like a mod file you add yourself.
{{% /tab %}}
{{% tab "From a file" %}}
A mod comes as one `.resteep` file (older mods: `.bbmod`; a `.zip` of either works too).

1. Open ReSteep's **Mods** page (**My mods**).
2. Press the **+** tile (**Add a mod file**) and choose the file. The mod gets a tile.

You can also put the file into the mods folder yourself (**Open mods folder** at the bottom of the page). ReSteep
unpacks it at the next Play.

On Linux, **Add a mod file** only adds mods that hold data and Lua scripts. A mod with native code or other scripts
is refused: put it into the mods folder yourself only if you trust its author.
{{% /tab %}}
{{< /tabs >}}

Then press **Play**. A new or changed mod is built before the game starts. This can take a few minutes; unchanged
mods start at once. Changes made while the game runs apply at the next game start.

Where the mods folder is: `%LOCALAPPDATA%\ReSteep\mods` on Windows, `~/.local/share/resteep/mods` on Linux.
**Settings → Mods folder** points ReSteep at another folder, for example a checkout of official-mods while you work on
mods.

## The Mods page

Each tile shows the mod's name, version and author, and what it contains: **Textures**, **Texts**, **Script**,
**Settings**, **Costumes**, **World**, **Server** or **Native code**.

- **The switch** turns the mod on or off.
- **Show items** (mods that add gear) lists the items, with a 3D view of each.
- **Settings** opens the mod's settings. A setting marked "Needs a game restart." applies from the next game start.
- **Remove** deletes the mod. Items it added leave your wardrobe; a rider wearing one gets the slot's default item.
- **A red line** is an error in the mod: it is not used until the mod is fixed.
- **Click a tile** for the mod's page: its picture, README, changelog, licence, the mods it needs, and **Update to …**
  when a newer version is out.

On Linux, a mod that needs it shows a **Build** or **Generate** link first: press it with the game closed. Remove a
mod by deleting its folder, and change its settings in the game.

### Mods that need a file you download

Some mods need a file their author may not hand out with them, a 3D model for example. Their tile says **Needs a file
you download**:

1. **Get the file** shows whose it is and its licence.
2. **Open the download page** opens the author's page in your browser. Download it there.
3. **Choose the downloaded file** takes the file you saved (usually a `.zip`).

ReSteep checks it (pictures and model files only) and keeps it for that mod. The mod is built with it at the next
Play.

## In the game: the MODS page

Press **N** and open **MODS**. Each mod has a line:

- **The checkbox** switches it on or off, the same switch as in the launcher. A script starts or stops at once; new
  gear, textures and world changes need a game restart.
- **The (i)** shows its description.
- **On the right:** the time its script takes per frame (`0.12 MS`), **CONTENT** (gear, textures or world only),
  **OFF**, or **ERROR** with the reason in red below.
- **RELOAD** starts its script again.
- **The gear** opens the mod's settings.
- **PANEL** shows a mod's own controls, when it has some (the [world editor](world-editor.md)'s are there).

At the bottom: **RELOAD ALL**, **REFRESH** (unpacks new mod files and reads the mods again), **OPEN FOLDER**,
**NATIVE MODS** and **CONSOLE** (what the mods log, with a line to run Lua in).

## Is it safe?

Most mods are data and Lua scripts in a sandbox, which can't open your files or start programs. Mods with native code
never load without your approval, and **a server can never push code to your game**. Details:
[Mod safety](safety.md).
