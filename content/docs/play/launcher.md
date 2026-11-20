---
title: The launcher
weight: 10
---

# The launcher

The ReSteep window is the same on Windows and Linux. Its pages:

| Page | What it is for |
| --- | --- |
| **Play** | What ReSteep checked (game, version, server, Ubisoft Connect), the **Play** button and the steps of a start. With both the Steam and the Ubisoft Connect version installed, it offers both. |
| **Mods** | Your mods with a switch each, their settings, and the **Official** and **Thunderstore** lists to install more: [Mods](../mods/). |
| **Server** | Your local server (hosting, players, kicks and bans) and the servers you join: [Playing with friends](multiplayer.md), [Hosting](../hosting/). |
| **Settings** | General settings, hotkeys, **Setup & repair** (what a start needs, backups, logs), and on Linux the Wine and Steep paths. |

## What Play does

Play goes through a few steps. Each one only checks, unless something is missing:

1. **Game files.** It finds Steep and Ubisoft Connect (and Steam for the Steam version) and checks that `Steep.exe`
   is the final update ReSteep supports.
2. **Firewall** (only when hosting or joining, Windows). Windows Firewall must let the other PCs in. ReSteep explains
   what it adds before Windows asks for admin rights. The rules allow only the local network, and only on networks
   Windows treats as private.
3. **Server.** It starts the local server, after checking that its ports are free, or reaches the server you join.
4. **Certificate.** It fetches the server's certificate authority and checks that it can only vouch for Ubisoft's
   names. The first time, it shows its fingerprint and asks you to trust it. Every server's certificate is pinned
   from then on: if it changes, Play stops with a warning.
5. **Account.** On your own server, ReSteep signs in with its own credentials. The first time you join another
   server, it [asks for your account there](multiplayer.md#your-account-on-a-server).
6. **Ubisoft Connect.** It starts Connect against the server and waits until Connect has signed in. Connect signs in
   by itself.
7. **Steep.** It starts the game, attaches ReSteep's parts to it and waits until the game is online.

Nothing on Windows is changed for this: ReSteep's hooks inside Ubisoft Connect and Steep point the Ubisoft names at
the server and trust only its pinned certificate. On Linux the game runs in a private session that leaves nothing
behind.

## Stop

While the game runs, the Play button is **Stop**. It asks first, because unsaved progress in the current run is
lost. Then it closes Steep the way its own close button does (and ends it if it has not quit after 15 seconds), stops
the local server and closes the Ubisoft Connect that ReSteep started. Your saves and data are never touched by Stop.

## Discord

ReSteep can show your Discord friends what you are doing: "In the launcher", or "Riding the Alps" with the server's
name. A server's address is never shown. Switch it off under **Settings → General → Discord Rich Presence**.

## Undo everything (Windows)

**Settings → Setup & repair → Undo everything** removes what any ReSteep version set up on this PC: hosts entries,
certificates and firewall rules. It asks before each Windows prompt and only acts if something is there, so it is
safe to run any time. Your progress is kept, and the next Play sets up again what it needs.

From a command prompt in the program's folder: `powder-cli.exe --status` shows what is set up, `--restore` undoes it.
