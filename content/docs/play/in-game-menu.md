---
title: The in-game menu
weight: 20
---

# The in-game menu

ReSteep's menu inside Steep opens with **N** or **Home**; **Esc** closes it. You can choose another key under
**Settings → General → Hotkeys → Open ReSteep menu**, in the launcher or in the menu's own Settings page. It runs on
Windows and on Linux (switch it off under **Settings → Linux → In-game menu**; Lua mods need it).

## Pages

| Page | What it has |
| --- | --- |
| **Gameplay** | Jump gravity, terminal velocity and more of the riding's values. These apply to this PC only. |
| **World** | The time of day, how fast time runs, and the world's presets (seasons). |
| **Movement** | **Fly** with noclip, a teleport spot, and saved positions. |
| **Mods** | Your mods: switch them on and off, their settings, panels and errors, and a console for mod makers: [Mods in the game](../mods/_index.md#in-the-game-the-mods-page). |
| **Profile** | Your player on the server. |
| **Server** | The servers you can join, and your own: [Playing with friends](multiplayer.md). |
| **Admin** | For the server's admins: players, credits and items, stats, messages to everyone: [Administration](../hosting/admin.md#the-admin-page). |
| **Debug** | What runs (hooks, fixes, mods), the server's broadcasts, HTTP activity and a memory scanner. |

## Fly

**F6** switches Fly on and off. Fly moves where the camera looks: **W A S D** to move, **Shift** up, **Ctrl** down.
With noclip, the game's physics and collision can't move you, so you pass through hills. The camera is found while
you play: turn it once while standing still.

## Always on

- **A crash log.** If the game crashes, the menu's log names where (`powder_overlay.log` beside the game on Linux,
  `native\bin\overlay.log` on Windows).
- **Small game fixes**, for example a guard against a crash in the DLC worlds.

The menu writes nothing else into the game folder.

> [!NOTE]
> The menu only works with the Steep build ReSteep knows (the final update). With another build it says "THIS STEEP
> BUILD IS NOT THE ONE RESTEEP KNOWS" and turns off the parts that need it. Let Steam or Ubisoft Connect update or
> verify the game.
