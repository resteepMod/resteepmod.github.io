---
title: The Lua API
weight: 30
---

# The Lua API

In-game scripts call ReSteep through the `resteep` table (API version 1: `resteep.info().api`). This page is an
overview of every area. The full reference, with every field and the calls already seen working in the game, is in
the ReSteep repository: `docs/modding/api.md` and `docs/modding/checked.md`.

## How scripts run

- **Lua 5.4 in a sandbox:** `string`, `table`, `math`, `utf8`, `coroutine` and the base functions. No `io`, `os`,
  `require`, `load`, `dofile` or `debug`, and no bytecode. A mod can't read or write files except its own save, and
  can't start programs.
- **Limits:** each mod has its own Lua state of at most 64 MB, and each call at most 20 ms (loading `main.lua`:
  200 ms). A mod that errors or runs too long is stopped; the MODS page shows why, and the other mods go on.
- **When:** once per game frame, on the game's own thread while you are in a world; in menus and while loading, from
  the renderer.
- **What stays local:** everything a mod changes stays on this PC, except what it sends to the server with
  `resteep.post` and `resteep.http`.

## Events

```lua
resteep.on("crash", function(info)
    resteep.log("crashed at " .. math.floor(info.speed) .. " m/s")
end)
```

| Event | Arguments | When |
| --- | --- | --- |
| `frame` | `dt` (seconds) | Every frame. Draw here. |
| `takeoff` / `landing` | `airtime` on landing | The rider leaves / is back on the ground |
| `landing_quality` | `{airtime, loss, vertical, speed, crash, ...}` | Shortly after a landing: how hard it was |
| `sport_change` | `{sport, previous, ...}` | `"snowboard"`, `"ski"`, `"wingsuit"`, `"paraglide"`, `"speedriding"`, `"sled"`, `"rocket_wingsuit"`, ... |
| `crash` / `crash_end` | `{sport, x, y, z, speed, air}` / `{duration}` | The rider falls / the ragdoll is over |
| `impact` | `{part, amount, material, x, y, z, cause}` | The game counted a hit of the rider |
| `key` | `name` | A key was pressed (game in front, menu closed) |
| `zone_enter` / `zone_exit` | `name` | The rider enters / leaves one of the mod's zones |
| `player_found` / `player_lost` | | The rider appears / is gone |
| `world_enter` / `world_leave` | | In a world / back in a menu |
| `config_change` | `key, value` | The player changed a setting |
| `panel` | | Every frame while the mod's panel shows ([UI](ui.md)) |

`resteep.emit(name, value)` sends an event of your own to every mod, next frame.

## The rider

| Call | Returns / does |
| --- | --- |
| `resteep.player()` | `nil` or `{x, y, z, velocity, speed, air, airtime, sport, ragdoll, ...}` (metres, Z up) |
| `resteep.sport()` | The current sport's name |
| `resteep.teleport(x, y, z [, vx, vy, vz])` | A small move on the ground |
| `resteep.rider.place(x, y, z)` / `.reset()` | Start over from a place, as "Try again" does / at the last spawn point |
| `resteep.rider.set_velocity`, `.add_velocity`, `.set_speed`, `.stop` | Change the velocity on the ground |
| `resteep.rider.hold(true)` / `.set_position(x, y, z)` / `.hold(false)` | Take the rider from the physics and move it freely (one mod at a time) |
| `resteep.rider.bone(name)` / `.bones([names])` | Where the rider's bones are (`"Head"`, `"LeftHand"`, ...) |
| `resteep.rider.damage()` | The game's damage count, where the mode keeps one |
| `resteep.rider.play_anim(from, to)` / `.stop_anim()` | Play another animation clip in place of one |
| `resteep.rider.anim_seen()` | Which clips the game looked up: to find the name for `play_anim` |

## Objects in the world

| Call | Returns / does |
| --- | --- |
| `resteep.prop.find(id)` | A handle for a loaded object the map places (by its id) |
| `resteep.prop.get(h)` / `.set(h, {x, y, z, yaw, matrix})` | Where it is / move it (call every frame to make it follow) |
| `resteep.prop.spawn(h, {...})` / `.unspawn(copy)` | A copy of a loaded object, placed in the world |
| `resteep.prop.bone(h, name)` / `.set_bone(h, name, {...}, "local")` | Read and move an object's bones (a helicopter's rotor) |
| `resteep.prop.keep(h)` | Leave a moved object where it is when the mod stops |

Everything a mod moved goes back when it stops, unless it kept it.

## The world

| Call | Returns / does |
| --- | --- |
| `resteep.world.name()` | `"STP_Alpes"`, `"STP_Japan"`, `"STP_Alaska"` or a custom map's name |
| `resteep.world.get()` | `{hour, paused, frozen, speed, weather, wind, preset, ...}` |
| `resteep.world.set_hour(h)`, `.pause(on)`, `.speed(x)` | The clock |
| `resteep.world.freeze(on)` / `.step(n)` | Stop the whole simulation / run `n` steps |
| `resteep.world.presets()` / `.set_preset(id)` | The world's seasons |
| `resteep.world.ground(x, y)` | The terrain's height |
| `resteep.world.raycast(...)` / `.spherecast(a, b, r)` | The game's own collision queries (what the rider hits) |
| `resteep.world.locations([kind [, map]])` / `.nearest(x, y, z)` | The game's places: drop zones, challenges, points of interest |
| `resteep.world.replay()` | Whether the game plays a replay |
| `resteep.gameplay.get(name)` / `.set(name, v)` / `.reset()` | Gravity, rider mass, stiffness: the Gameplay page's values |
| `resteep.handling.get(name)` / `.set(name, t)` / `.reset(name)` | The game's riding tables (snowboard, ski, sled, ...) |
| `resteep.domino.list()` / `.start(id)` / `.stop(id)` | Run the game-engine scripts the mod placed |

## Zones, timers and keys

| Call | Returns / does |
| --- | --- |
| `resteep.zone(name, x, y, z, radius)` / `resteep.remove_zone(name)` | A sphere that fires `zone_enter` / `zone_exit` |
| `resteep.after(s, fn)` / `resteep.every(s, fn)` / `resteep.cancel(id)` | Timers |
| `resteep.time()` | Seconds of game frames since the mods started |
| `resteep.held(name)` | Is a key held? Names: `A`..`Z`, `0`..`9`, `F1`..`F24`, `SPACE`, `SHIFT`, `UP`, ... |
| `resteep.info()` / `resteep.version()` | Where the script runs; ReSteep's version |

Avoid the game's own keys and ReSteep's menu key (N by default).

## Input for the game

Call these every frame for as long as they should be held. The game gets the real input back within a quarter
second after the mod stops.

| Call | Does |
| --- | --- |
| `resteep.input.pad{lx, ly, rx, ry, lt, rt, buttons = {...}}` | Replaces the gamepad for this frame |
| `resteep.input.key(name, ...)` | Holds keyboard keys for this frame |
| `resteep.input.read()` | The real gamepad (the one used last) |
| `resteep.input.mouse()` | How far the mouse moved |
| `resteep.input.capture(on [, "pointer"])` | The game gets no keyboard and mouse while the mod uses them |
| `resteep.input.pointer()` | The mouse pointer over the overlay |

## Drawing and the camera

Call these in the `frame` event. Screen positions are fractions of the window (0..1); colours `"#RRGGBB"`,
`"#AARRGGBB"` or `0xAARRGGBB`.

| Call | Does |
| --- | --- |
| `resteep.text(x, y, text [, color [, size]])` | Text, centred at x |
| `resteep.box(x, y, w, h [, color])` / `resteep.line(...)` | A filled box / a line |
| `resteep.marker(x, y, z [, label [, color]])` | A ring at a place in the world |
| `resteep.project(x, y, z)` | Where a world position is on screen |
| `resteep.notify(text [, seconds])` | A short note at the top |
| `resteep.hud.notify(text)`, `resteep.hud.banner(title, sub)` | The game's own notification and result banner |
| `resteep.hud.hide(on)` | Hide the game's HUD (for photo and camera mods) |
| `resteep.camera()` | The camera: position, direction, field of view |
| `resteep.camera.tweak{...}` / `resteep.camera.set{...}` | Change the game's camera, or replace it, renewed every frame |
| `resteep.sound.play(file, {loop, volume, pitch, at, range})` | Play a WAV file of the mod, in the world or flat |

## Saving and the server

| Call | Does |
| --- | --- |
| `resteep.save(value)` / `resteep.load()` | Keep data (up to 4 MB) in the mod's `save.lua` |
| `resteep.config.get(key)` / `.set(key, v)` / `.all()` | The mod's [settings](format.md#settings) |
| `resteep.log(...)` / `print(...)` | A line in the MODS console |
| `resteep.post(path, table [, fn])` | A call to the server the game is on |
| `resteep.http(method, path [, body [, fn]])` | A call to the mod's own [server half](server-mods.md), under `/_powder/<mod id>/` |
| `resteep.data.read(name)` / `.json(name)` | Files a build step wrote for the mod at the game's start |

Every mod has its own leaderboards on the server, with no setup:

```lua
resteep.post("/mods/board/submit", {board = "longest-air", value = airtime, lower_is_better = false},
    function(ok, reply)
        if ok and reply.improved then resteep.notify("New best! Rank " .. reply.rank) end
    end)
```

`/mods/board/top {board, limit}` reads the top of a board. Boards count only on that server, and take the value as
the mod sends it.
