---
title: Windows
weight: 10
---

# ReSteep on Windows

## Install

1. Download `ReSteep-Setup-vX.Y.Z.exe` from the [releases page](https://github.com/resteepMod/ReSteep/releases) and
   run it.
2. Choose who it is for:
   - **For all users** (the default): installs into Program Files. It needs admin rights at install and at each
     update, so no other program can change ReSteep itself.
   - **Only for you**: installs into `%LOCALAPPDATA%\Programs\ReSteep`, without admin rights.
3. ReSteep is not code-signed yet, so Windows SmartScreen may warn about an unknown app. Choose **More info**, then
   **Run anyway**.

Your progress, settings and mods live apart from the program, in `%LOCALAPPDATA%\ReSteep`. Installing a newer
version over the old one never touches them. ReSteep tells you on its Play page when a new version is out:
**Download**, then **Restart and update**.

## First Play

Start **ReSteep**. The **Play** page lists what it checked: the game found, its version supported, the local server,
Ubisoft Connect. Press **Play**.

A card shows each step while the game starts. When a step needs you, ReSteep stops and explains why before Windows
asks anything. On a first start you may see:

| Prompt | What it means |
| --- | --- |
| **Restart Ubisoft Connect** | Connect was already running, signed in elsewhere. ReSteep restarts it against its server. If Connect then asks you to sign in, type anything: this PC signs in as its own player. |
| **Fix it / Not now** | Ubisoft Connect asks for admin rights at every start because a runtime it keeps reinstalling is broken. ReSteep can repair it once. |
| **Add firewall rules / Skip** | Only when you host for friends. Windows asks for admin rights. |
| **Check again** | Another program uses the local server's ports. ReSteep names it: close it and press Check again. |

ReSteep minimizes while the game runs and comes back when you quit.

> [!NOTE]
> Closing ReSteep while Steep runs stops the local server, so the game goes offline. ReSteep asks first.

What Play does step by step is described in [The launcher](../play/launcher.md#what-play-does).

## The in-game menu

Press **N** (or **Home**) in the game to open ReSteep's menu; **Esc** closes it. If you use N for something in the
game, choose another key under **Settings → General → Hotkeys → Open ReSteep menu**. More:
[The in-game menu](../play/in-game-menu.md).

## Uninstall

ReSteep changes nothing in Windows to play: Ubisoft Connect talks to ReSteep's server only while ReSteep starts it,
and to Ubisoft's servers otherwise. The only thing it may add are firewall rules, when you host or join
([What ReSteep leaves on Windows](../play/launcher.md#what-resteep-leaves-on-windows)).

**Uninstall** ReSteep in Windows Settings → Apps. If you added firewall rules, it removes them first. Your progress,
settings and mods are kept unless you tick **Also delete my ReSteep data**.
