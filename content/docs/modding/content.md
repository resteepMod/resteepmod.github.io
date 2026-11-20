---
title: Content
weight: 50
---

# Content mods

A mod's `content` in `resteep.json` declares what it adds to or changes in the game. The launcher builds it when the
game starts, **from the player's own install**: a mod carries only its own files (pictures, glTF models, JSON), never
the game's. Nothing in the game folder is written; the built archives are handed to the game for that session.

Content changes need a game restart. The pages below give an overview; the ReSteep repository's `docs/modding/`
and `tools/forge/` have every field.

## Textures and texts

```json
"content": {
  "textures": [{"target": "0x78fd63167d", "file": "textures/base.png", "tint": "${color}", "if": "paint"}],
  "strings":  [{"id": "0x2f74", "text": {"en": "GREY BEANIE DELUXE", "de": "GRAUE MÜTZE DELUXE"}},
               {"key": "cap_name", "text": "${name}"}]
}
```

- **Textures:** `target` is a texture's name or id. The picture replaces it at its size and format; compression and
  mip maps are made for you.
- **Strings:** `id` is one of the game's texts (find them with `python -m resteep strings find "grey beanie"`); `key`
  adds a new one. One text for every language, or one per language.

When two mods replace the same texture or text, the later one wins and both show a note.

## Items and costumes

```json
"items":    [{"key": "shell", "slot": "jackets", "title": "Neon Shell", "model": "models/shell.glb"}],
"costumes": [{"name": "COSTUME_MF_NEON_SUIT", "like": "COSTUME_MF_URBAN_OUTFIT_BIB_131",
              "title": "Neon Suit", "icon": "assets/icon.png", "grant": true}]
```

New wardrobe items with their own models and textures, and whole costumes. An item's id comes from the mod's id and
the item's `key`, so it is the same on every PC: **keep both across versions**, since a save stores equipped items by
id. A costume can also be **fitted from a download**: the build fits a rigged model the player downloaded onto
Steep's skeleton on their PC, so the mod never passes the model on.

Models come from Blender as glTF (`.glb`). The ReSteep repository's Blender add-on and `tools/forge/BLENDER.md`
show how to start from a game item with its armature and weights.

A **build script** (`"build": "build.lua"`) computes items and challenges in a sandbox (no files, network or
programs) while the content is built.

## World edits and new maps

```json
"worlds": [{"map": "Alpes", "edits": "assets/park.json", "models": {"hut": {"glb": "models/hut.glb"}}}],
"maps":   [{"world": "STP_Template_2km_2km", "from": "WhiteRoom", "title": "RESTEEP PARK",
            "edits": "assets/park.json", "drop_zone": [60, -10, 21]}]
```

- **Worlds** change the Alps, Japan or Alaska: objects added, moved or removed (the
  [world editor](../mods/world-editor.md)'s edits), with the mod's own models.
- **Maps** are new worlds of their own, a fourth massif next to the Alps, Asia and Alaska: a copy of a shipped map,
  or part of one, with edits on top, drop zones, points of interest, challenges and a postcard for the world page.
- A map can have **its own terrain** over its whole 16 km square: generated from a seed
  (`{"generate": {"seed": 7, "low": 1200, "high": 3900}}`) or from a grey heightmap picture.

Maps and world edits are always shared: every player on a server needs the same.

## Challenges

```lua
resteep.challenge{
  key = "downhill", kind = "race", map = "Alpes",
  title = {en = "Downhill", de = "Abfahrt"},
  start = {-617.6, -6126.4, 1456},
  elements = {
    {type = "checkpoint", at = {-736.2, -6051.7, 1401.2}, range = 10},
    {type = "finish", at = {-858.4, -6092.0, 1345.4}},
  },
  medals = {30, 40, 55},
  rewards = {{credits = 800}, {credits = 600}, {credits = 400}},
}
```

Open-world challenges of every kind the game has (race, score, jump, fall, reach), built like the shipped ones:
a start marker on the map, gates, medals, rewards and a leaderboard of their own. Declare them in
`content.challenges` or compute them in a build script, as above. `resteep.player()` in the console shows the
coordinates where you stand.

## Music

```json
"music": [
  {"key": "theme", "file": "music/theme.ogg"},
  {"key": "calm", "file": "music/calm.wav", "challenges": ["A19_P_BUTTERFLY"], "if": "replace_butterfly"}
]
```

A mod's own tracks (WAV, OGG, MP3 or FLAC, up to 20 minutes) for its challenges, or in place of a shipped challenge's
music. Share only music you may share.

## Animations

```json
"animations": [
  {"replace": ["ID00_PS00_male_GRAB_INDY", "ID00_PS00_female_GRAB_INDY"], "file": "anims/indy.glb"},
  {"replace": "ID01_PS00_male_GRAB_MUTE", "clip": "ID01_PS00_male_DOUBLEGRAB_TRUCKDRIVER", "speed": 1.5}
]
```

Replace one of the game's animation clips with another clip of the game, or with an animation made in Blender. The
trick keeps its name and points; only what you see changes. `resteep.rider.anim_seen()` lists the clips a move
plays.

## Scripts in the world

`content.scripts` places scripts of the game's own script engine (node graphs) on a map: spawn an object, move it,
show a tooltip, change the time of day. Lua then starts and stops them with `resteep.domino`. They never touch
unlocks, rewards, challenges or stats. This is experimental; `official-mods/mods/domino_showcase` shows what works.
