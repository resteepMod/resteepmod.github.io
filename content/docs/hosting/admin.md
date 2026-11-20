---
title: Administration
weight: 20
---

# Administration

## Server commands

The server is one program, `powder-server`: `powder-server.exe` beside `ReSteep.exe` in the installed Windows program,
`target/release/powder-server` in a checkout. It reads `./config.toml` unless given another with `-c`. For the
installed program's data:

```
powder-server.exe -c "%LOCALAPPDATA%\ReSteep\config.toml" admin players
```

{{% details title="All admin commands" open=false %}}
```
powder-server admin players
powder-server admin inventory              # item count and credits
powder-server admin grant credits 50000    # or an item id; negative to remove
powder-server admin stats --key level
powder-server admin ledger                 # recent inventory changes
powder-server admin rewards [--pay]        # rewards earned before they were paid: list, or pay them once
powder-server admin offers armada          # search the store catalogue
powder-server admin events                 # recent progress uploads from the game
powder-server admin scores                 # personal best per challenge
powder-server admin entities               # rider card, favourites
powder-server admin achievements --all
powder-server admin cloud-saves [PLAYER] --delete
powder-server admin world-edits [--map M] [--by PLAYER] [--export edits.json]
powder-server admin import <recordings>
powder-server admin reset                  # the player starts again as a new player
powder-server admin trust status           # the local certificate authority in Windows
```
{{% /details %}}

Commands work on the default player unless a player is given. Other commands:

```
powder-server run                     # the server alone
powder-server mods                    # load the mods and show what they hook
powder-server gamedata verify         # also build / zip / install
```

> [!WARNING]
> Never change a player's level or unlock stats by hand: the game checks its saves against them, and the first-time
> intro comes back.

## Bans, the whitelist and kicks

```
powder-server admin bans                                       # the bans and the whitelist
powder-server admin ban PLAYER [--for 7d] [--reason TEXT]      # 30m, 12h, 7d, 2w; default: until unbanned
powder-server admin unban PLAYER
powder-server admin ban-ip ADDRESS[/PREFIX] [--for 7d]         # 192.0.2.7, 192.0.2.0/24, 2001:db8::/32
powder-server admin unban-ip ADDRESS
powder-server admin kick PLAYER [--reason TEXT]                # they may sign in again
powder-server admin whitelist on|off|add PLAYER|remove PLAYER|list
```

- Players are named by profile id, account email or player name.
- A banned player, or anyone from a banned address, can't sign in, register, or use a ticket they already have.
- While the whitelist is on, only its players and the server's admins get in.
- A kick ends the player's sessions and connections; unless banned, they can sign in again at once.
- The server's admins are exempt from the whitelist and address bans and can't be banned, so a host can't lock
  themselves out.

The rules live in the server's database: the command line, the admin page and the launcher's Server page change the
same list, and a running server applies changes within about 5 seconds.

## The admin page

The admin page at `https://<server>/_powder/admin` is for the server's admins: players and who is online, inventory,
credits and items, stats, resetting a player, messages to everyone online, bans, the whitelist and kicks.

List the admins' profile ids (`powder-server admin accounts` shows them) in `config.toml`, and sign in on the page with
that account's email and password:

```toml
[server]
admins = ["<profile id>"]
```

**The host needs no password.** In the game on the server's own PC, the in-game menu's **ADMIN** page signs the host
in by itself. Only the launcher that runs the server can ask for that session (with a token only it can read), and the
session works only from the server's own PC.

From the server's PC the page is at `https://127.0.0.1:<https_port>/_powder/admin`. The browser doesn't know the
server's local certificate authority: accept the warning, or import `data/tls/ca.pem`.

## The world editor

The [world editor](../mods/world-editor.md) lets players change the world from the in-game menu. By default only the
server's admins may edit, and every edit records who made it. Set the rules in `config.toml`:

```toml
[mods.settings.world_editor]
edit = "everyone"          # who may edit: "admins" (default), "everyone" or "off"
undo_others = true         # players may undo or change other players' edits
shipped_objects = true     # players may move or remove the game's own objects
max_adds = 0               # objects per player (0: no limit); max_edits likewise
blocked_props = ["Sapin"]  # parts of prop names players may not place
```

Admins can also change them in the game (the editor panel's **Server rules (admin)**); those win over `config.toml`.
`powder-server admin world-edits --export edits.json` writes the edits out, to make a mod of them with the ReSteep
repository's `tools/forge/worldblend.py`.
