---
title: The world editor
weight: 20
---

# The world editor

Add objects to Steep's world, and move, turn, scale or remove the ones that are there, from inside the game. The
server you play on keeps your edits, so they are still there at the next start.

> [!WARNING]
> The world editor is new and experimental. It has been used on Linux; Windows is not tried yet. Read
> [Limits](#limits) before you build something big.

## Switch it on

1. Install **World editor** from the launcher's **Mods → Official** tab.
2. If its tile shows a **Build** link, press it (with the game closed) and wait until the build is done.
3. Switch the tile on. The in-game menu is switched on with it.
4. Press **Play**. The first start reads each map's objects once (about 20 seconds for an open-world map).

Don't switch it on together with the `asset_trace` research mod: both change the same part of the game.

## Open it

Press **N**, open **MODS**, and find the **World editor** card; its **PANEL** is below it. The panel has:

- **The map**: Alpes, Japan, Alaska or WhiteRoom (the main menu's scene).
- Your position and the 128 m square ("cell") you are in.
- **Free camera (edit with the mouse)**: the easiest way to edit.
- **Add an object**: a list of objects to place.
- **Objects near you**: to change them with buttons.
- **Edits**: every edit of the map, newest first, with undo.

## Editing with the free camera

Press **Free camera**. The menu closes, the world holds still, and a small window shows what is selected. The keys
are like Blender's:

| To | Do this |
| --- | --- |
| Look around and fly | Hold the **right mouse button** and move the mouse; fly with **W A S D**, **Q**/**E** down/up (**Shift** fast, **Ctrl** slow, the **wheel** sets the speed) |
| Orbit around the selection | Hold the **middle mouse button** |
| Pan | **Shift** + middle mouse button |
| Zoom | The mouse **wheel** |
| Look at the selection | **F** or **Numpad .** |
| Select an object | Point at it and **click** |
| Move / turn / scale | **G** / **R** / **S** |
| Duplicate and move the copy | **Shift + D** |
| Place the object chosen in the panel | **Shift + A** |
| Put it onto the ground | **End** |
| Remove it | **X** twice, or **Delete** |
| Undo your last edit | **Ctrl + Z** |
| Leave the free camera | **Esc** |

While you move, turn or scale:

- **X**, **Y** or **Z** locks to the map's axis; again to the object's own axis; once more frees it. **Shift + X/Y/Z**
  leaves that axis out (Shift + Z moves along the ground).
- Type a number for an exact amount (metres, degrees or a factor).
- Hold **Ctrl** to snap (0.5 m, 5 degrees, 0.1).
- **Click** or **Enter** saves the edit; **right click** or **Esc** cancels it.

The camera can fly anywhere, but the game only loads the world around your rider (about 700 m). Edits far away show
once your rider comes near.

## Editing with the panel

- **Add an object:** type in the filter (`sapin` for firs, `rock`, `kick`, `bench`), pick an object, set its distance,
  height, turn and scale, and press **Add here**.
- **Change an object near you:** choose it under **Objects near you**, then **Move**, turn, scale, **Onto the
  ground** or **Remove**. A far move is better done as remove and add.

## Saving and undo

There is no save button: every edit goes to the server at once. **undo** next to an edit takes it back, **Undo last**
(or **Ctrl + Z**) your newest one. **Clear all…** removes every edit of the map (server admins only).

## On a server

Every edit records who made it. By default only the server's admins may edit; on your own server you are the host.
Admins can let everyone edit, set limits per player and remove a player's edits (**Server rules (admin)** in the
panel, or [in the server's config](../hosting/admin.md#the-world-editor)).

Players who join with the world editor switched on (Linux) get the server's edits when the game starts. Players
without it, and players on Windows, don't see them yet.

## Limits

- Added objects are experimental: copies of some objects show a long thin white bar.
- Trees and rocks the game places in bulk can't be edited yet.
- Objects stand on the terrain only when you ask (**End**, **Onto the ground**).
- An edit in a map's biggest cell can take about 17 seconds to show.
- A server keeps at most 2000 edits.
- Turning your edits into a mod others can install is not in the game yet. A host can export them:
  [The world editor on your server](../hosting/admin.md#the-world-editor).
