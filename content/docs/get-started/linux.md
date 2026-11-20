---
title: Linux
weight: 20
---

# ReSteep on Linux

On Linux, ReSteep is a single file, an AppImage: there is nothing to build and no packages to install. It changes
nothing on your system. The server and its certificate exist only inside each game session.

## Install

1. Download `ReSteep-vX.Y.Z-x86_64.AppImage` from the
   [releases page](https://github.com/resteepMod/ReSteep/releases). You can check it against the release's
   `SHA256SUMS`.
2. Make it executable (your file manager's **Properties → Allow executing**, or
   `chmod +x ReSteep-*.AppImage`) and start it.

The first start adds ReSteep to your application menu. Your settings, mods, server data and the game setup ReSteep
makes go to `~/.local/share/resteep`. Never run ReSteep as root.

The system needs only what every desktop has: `unshare` (util-linux) and `ip` (iproute2). Joining or hosting a
server also uses `pasta` (package `passt`) and `nft` (`nftables`).

> [!NOTE]
> **Ubuntu 23.10 and newer** need a one-time AppArmor profile for ReSteep. ReSteep tells you when it is missing;
> the steps are in [Troubleshooting](../troubleshooting/_index.md#ubuntu-user-namespaces). On a system without FUSE
> (some containers), start the AppImage with `APPIMAGE_EXTRACT_AND_RUN=1`.

## First Play

1. **Ubisoft Connect.** If you already have it in a Wine prefix (from Lutris, for example, in `~/Games`), or Steep
   from Steam (its Proton prefix has Ubisoft Connect once Steam has started the game), ReSteep finds it.
   Otherwise open **Settings → Setup & repair** and press **Install Ubisoft Connect**. It downloads umu-run,
   GE-Proton and Ubisoft Connect into `~/.local/share/resteep`. If that fails, install Ubisoft Connect with Lutris.
2. **Steep.** Press **Open Ubisoft Connect** on the same page, sign in with your Ubisoft account and install Steep.
   If Steep is installed but not found, press **Choose folder** next to "Steep not found" on the Play page and pick
   the folder with `steep.exe`. If ReSteep picks the wrong place, set **Wine prefix** or **Steep folder** under
   **Settings → Linux**.
3. **Play.** ReSteep starts Ubisoft Connect and Steep. You can close the window while the game runs.

## Steep from Steam

Steep bought on Steam has to be started by Steam, or Ubisoft Connect asks for an activation code. The Play page then
shows **Play through Steam** with **Set up**:

1. ReSteep gives you one line to paste into Steam: **Steep → Properties → General → Launch options**.
2. Press **Done**.

From then on **Play** asks Steam to start Steep, and Steam runs ReSteep around it: the local server, your mods and
your settings. Starting Steep from Steam's own Play button does the same. Use the Proton you set for Steep in Steam
(GE-Proton11-11 is the one tested).

To go back, empty the launch option in Steam and switch **Play through Steam** off under **Settings → Linux**. From a
terminal, `ReSteep cli steam-setup` prints the line.

## How Linux differs from Windows

- **Nothing to undo.** A session leaves nothing behind on the system.
- **Hosting** uses one port of your choice (8443 by default) and needs no root:
  [Hosting on Linux](../hosting/_index.md#hosting-on-linux).
- **Switching servers** restarts Steep: the game's network is set up when it starts.
- **Mods** are the folders in `~/.local/share/resteep/mods`. A mod that needs it shows a **Build** or **Generate**
  link first. The window adds mod files that hold only data and Lua.
- **Updates:** the window offers a new release when there is one, checks its signature, replaces the AppImage you
  started and starts the new one when you close the window.

## Graphics options

Steep draws through DXVK (Direct3D on Vulkan) on Linux. Under **Settings → Linux**:

- **DXVK options** takes the lines of a `dxvk.conf`, separated by `;`, for example
  `dxvk.enableGraphicsPipelineLibrary = False`.
- **Wine environment** takes extra variables, as Steam's launch options would, for example
  `PROTON_ENABLE_NVAPI=1;DXVK_HUD=fps`.

Both apply from the next Play; empty them to undo.
