---
title: Coming from Powder
weight: 40
---

# Coming from Powder

ReSteep continues [Powder](https://github.com/Toemmsen96/powder), merged with BlueBird's launcher window, in-game menu
and Lua mods. Powder's parts keep their names inside ReSteep: the server is still `powder-server`, the Linux session
`powder-wrap`, and the server's own routes are under `/_powder/`.

## What is different

| | Powder | ReSteep |
| --- | --- | --- |
| **Windows setup** | Wrote a block into the hosts file and installed its certificate authority into your user's trusted roots | Changes neither: the Ubisoft names are pointed at the server and its certificate trusted inside Ubisoft Connect and Steep only, while ReSteep runs them. Only firewall rules remain, when you host or join |
| **Server** | The installed program ran the Python server | The Rust server only |
| **Launcher** | Powder's own window | ReSteep's window (from BlueBird): Play, Mods, Server and Settings pages, the same on Windows and Linux |
| **Linux** | Built from the source code | One AppImage, nothing to build; the session itself works as before |
| **Accounts** | One account, registered in Powder's launcher | Your own account per server: the first time you join one, you create it or sign in with one you have there |
| **In-game menu** | Powder's overlay (admin, trainer, client mods) | One menu (**N** or **Home**) with Powder's pages and BlueBird's: gameplay and world settings, Lua mods, profile, servers |
| **Mods** | Server mods, client DLLs, asset mods | Also sandboxed Lua mods in the game, content mods (items, maps, challenges, music, animations), the `.resteep` format, and the launcher's Official tab |
| **Challenge rewards** | Needed the game-data pack | Paid from the game's own reward packs, no pack needed |
| **Your data** | `%LOCALAPPDATA%\Powder` | `%LOCALAPPDATA%\ReSteep` |

## Moving from Powder to ReSteep (Windows)

1. **Undo Powder's setup.** In Powder, use **Restore system**. If Powder is already gone, ReSteep's **Settings →
   Setup & repair → Undo everything** finds what it left too: its hosts-file block, its certificate authority and its
   firewall rules.
2. **Bring your progress along, before the first Play.** Install ReSteep, then run once, from a command prompt in
   ReSteep's program folder:

   ```
   ReSteep.exe --import-data "%LOCALAPPDATA%\Powder"
   ```

   It copies your account, progress, cloud saves, the server's keys and certificates and the launcher's settings into
   ReSteep's folder. Powder's folder is only read. It refuses if ReSteep already has data, so nothing is overwritten.
3. **Play** with ReSteep. Once your progress is there, uninstall Powder.

> [!WARNING]
> Don't skip step 2 and play first. A new, empty data folder makes the server give you a new player, which has no
> save, so the game starts its first-time intro again.

## From a Powder checkout

On Linux or from the source code, copy your Powder checkout's `data/` folder into the ReSteep checkout before the
first Play, or point `--import-data` at the checkout. Mods in Powder's layout (`content.toml`, `mod.toml`) still load;
`python -m resteep convert` turns them into the new format ([Publishing](../modding/publishing.md)).
