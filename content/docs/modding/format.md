---
title: The mod format
weight: 20
---

# The mod format

One format for every kind of mod: a **folder** in the mods folder, or the same files as a **`.resteep` bundle** (a zip)
to share. It is Thunderstore's package layout, so Thunderstore, mod managers and mod packs work the same way, plus
ReSteep's own manifest, `resteep.json`.

```
mods/
  neon-jacket/
    manifest.json      Thunderstore: name, version, description, dependencies
    icon.png           256 x 256 PNG
    README.md          shown by mod managers and the launcher's mod page
    CHANGELOG.md       optional: what changed per version
    resteep.json       ReSteep: id, title, settings, content, scripts
    main.lua           optional: the in-game script
    mod.lua            optional: the server script
    textures/ models/  the mod's own files (PNG, glTF .glb, JSON, ...)
  neon-jacket-1.2.0.resteep   the same as a bundle: the launcher unpacks it to neon-jacket/
```

## manifest.json

Thunderstore's fields, checked by their rules:

```json
{
  "name": "Neon_Jacket",
  "version_number": "1.2.0",
  "website_url": "https://example.org",
  "description": "Paints the jacket.",
  "dependencies": ["ReSteep-ReSteep-0.1.0"],
  "author": "MyTeam"
}
```

| Field | Rules |
| --- | --- |
| `name` | `A-Z a-z 0-9 _`, up to 128 characters |
| `version_number` | `Major.Minor.Patch` |
| `website_url` | empty, or an `http(s)` address |
| `description` | up to 250 characters |
| `dependencies` | `Team-Name-Version`, the oldest version that works. `ReSteep-ReSteep-X.Y.Z` names the oldest ReSteep. |
| `author` | optional: your Thunderstore team |

## resteep.json

```json
{
  "format": 1,
  "id": "neon-jacket",
  "title": "Neon Jacket",
  "author": "Name",
  "license": "CC-BY-4.0",
  "resteep": "0.1",
  "tags": ["cosmetic"],
  "settings": [
    {"key": "color", "type": "color", "label": "Colour", "default": "#ff6a00"}
  ],
  "content": {
    "textures": [{"target": "0x78fd63167d", "file": "textures/base.png", "tint": "${color}"}]
  }
}
```

| Field | What |
| --- | --- |
| `id` | Required. `a-z 0-9 . _ -`, 3 to 64 characters. The folder it installs as: **never change it**, settings are stored under it. |
| `title` | The name players see (default: the manifest's name). |
| `author`, `license` | Shown on the mod's page. |
| `resteep` | The oldest ReSteep release the mod needs, e.g. `"0.1"`. |
| `icon` | Default `icon.png`. |
| `script` | The in-game script, default `main.lua` when it exists. |
| `server` | The server script, default `mod.lua` when it exists. |
| `sync` | `"synced"` (every player on a server needs it) or `"client"` (nobody does); see [Mods in sync](#mods-in-sync-with-a-server). |
| `tags` | Up to 8 short words; `developer` marks a tool for mod makers. |
| `downloads` | Files the player downloads themselves, e.g. a model under a licence that doesn't allow sharing it. |
| `settings` | What the player can change: [Settings](#settings). |
| `content` | What the launcher builds: [Content](content.md). |
| `native` | Client DLLs. Only loaded after the player approved them, and never in shared mods. |

## Settings

A mod declares its settings, and players change them in the launcher or on the in-game MODS page.

| Type | Value | Extra fields |
| --- | --- | --- |
| `toggle` | true / false | |
| `slider`, `number` | a number | `min`, `max`, `step`, `unit` |
| `choice` | one of `options` | `options`: strings or `{"value", "label"}` |
| `text` | a string | `max_length` |
| `color` | `"#rrggbb"` | |
| `key` | a key name such as `"F5"` | |

Every setting has `key`, `label`, `info` (shown at its **i**) and `default`. A value that doesn't fit its type falls
back to the default.

**In a script:** `resteep.config.get(key)`, `resteep.config.all()` and `resteep.config.set(key, value)`. When the player
changes a setting, the script gets the event `config_change(key, value)`.

**In content:** a mod without a script steers how its content is built. In a texture entry, `${key}` inside `file`
inserts a setting's value, `"tint"` multiplies the picture by a colour and `"brightness"` by a number, and
`"if": "key"` (or `"!key"`) includes the entry only while that toggle is on (off). Content changes need a game restart;
script-only settings apply at once.

## Mods in sync with a server

What players share must be the same on the server and on every player's PC, or the game desyncs: a player falls
through ground another sees, or an item id is missing on the other side.

- **Shared:** maps, worlds, scripts placed in the world, costumes, items, challenges and build scripts.
- **Not shared:** textures, strings, music and animations (they change what this PC draws), the in-game script, the
  server script and native code.

`"sync"` overrides this for a mod. The server publishes the mods it runs, each with a fingerprint of its files, and
the launcher compares them with the player's when they join. It never switches a mod on or downloads one by itself.

> [!TIP]
> Share mods as `.resteep` bundles. A git checkout that turns line endings into CRLF changes a mod's fingerprint.
