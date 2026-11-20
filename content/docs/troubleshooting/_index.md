---
title: Troubleshooting
weight: 60
bookFlatSection: true
---

# Troubleshooting

**First, open Settings → Setup & repair.** It lists what a start needs and offers to fix what is missing: **Repair
all** on Windows, the setup buttons on Linux. A **Repair** link on the Play page leads there too.

If nothing here helps, [save your logs and report the problem](logs.md).

## Starting the game

**"Steep not found".** Install Steep through Ubisoft Connect or Steam. If it is installed, on Linux press **Choose
folder** on the Play page and pick the folder with `steep.exe`.

**"Unsupported version".** ReSteep only starts Steep's final update (TU7). Let Steam or Ubisoft Connect update or
verify the game.

**The local server can't start.** Another program uses its ports (TCP 443 and 80, UDP 6005, 11000-11003 and 11005).
ReSteep names the program: close it and press **Check again**.

**"Ubisoft Connect did not sign in within 10 minutes".** If Connect asks you to sign in on your own server, type
anything: this PC signs in as its own player. On a server you joined, type the account you made there. Then press
**Play** again.

**"Steep did not start".** ReSteep asked Steam or Ubisoft Connect to start Steep, and the game didn't appear within 3
minutes. See whether Steam or Connect shows a message (an update, a question), then press **Play** again.

**"Is an earlier Steep still running?".** A Steep from an earlier start is still open, maybe hidden. Close it (Task
Manager if needed) and press **Play** again.

**"Steep closed while it was starting", "game closed before going online".** Press **Play** again. If it keeps
happening at the loading screen, see [below](#the-game-crashes-at-the-loading-screen).

**Ubisoft Connect asks for admin rights at every start.** Press **Fix it** when Play offers it, or in Setup & repair.

**A certificate warning when joining.** A server you trusted now shows a different certificate. Either its host made
a new one, or someone is listening in. Ask the host before you continue.

### Ubuntu: user namespaces

**"This system does not let programs make user namespaces".** Ubuntu 23.10 and newer only allow them for programs
with an AppArmor profile, and both Proton and ReSteep's game session need them. Put ReSteep's in place once:

```
sudo tee /etc/apparmor.d/resteep <<'EOF'
abi <abi/4.0>,
include <tunables/global>

profile resteep @{HOME}/.local/share/resteep/app/*/ReSteep flags=(unconfined) {
  userns,
  include if exists <local/resteep>
}
EOF
sudo apparmor_parser -r /etc/apparmor.d/resteep
```

It allows the program the AppImage unpacks into your data folder (and what it starts) to make user namespaces, and
nothing else. Then press the button again.

### Linux: Steep closes a few seconds after it starts

ReSteep's certificate fix has to come after the game's own tamper check, so it waits until the game starts its
networking. If `powder_tls.log` (next to `Steep.exe`) ends with `patched ssl_verify_cert_chain ... ok` and nothing
after it, start ReSteep with `POWDER_TLS_DELAY_MS=20000` set, and report it.

## In the game

### The game crashes at the loading screen

A save that grew too big over many hours of play could crash the game on the loading screen. ReSteep now shortens
that part of the save before every Play and keeps the old files. If it still crashes:

1. Make sure you start Steep with ReSteep's **Play**, not on its own.
2. Restore a save backup from before the problem: [Progress and saves](../play/progress.md#backups).
3. If that doesn't help, [report it](logs.md).

### The game goes offline

- **You closed ReSteep while the game ran** (Windows): that stops the local server. Start again with **Play**.
- **Linux, a key pressed on the title screen** too early can leave the game offline ("DE-014-01"). While the
  in-game menu shows "Connecting to the server…", wait for it to go away.
- **"No item list" (DE-010-01 right after signing in).** Steep keeps a copy of Ubisoft's item list from the last time
  it was online. A Steep that was never online on this PC has none, and ReSteep can't ship Ubisoft's list. Copy the
  game's `Documents/My Games/STEEP` folder from a PC where Steep has been online, or install a
  [game-data pack](../hosting/game-data.md).
- **After a server served a custom item list.** Once the game has taken such a list (`item_list.json` in the
  server's `data` folder), it needs one every time. Keep that file, and take it along to a new PC (**Export progress**
  has it).

### Linux: graphics crashes or a black screen

A new GPU or driver can crash with one of DXVK's newer features. Try `dxvk.enableGraphicsPipelineLibrary = False` in
**Settings → Linux → DXVK options**: [Graphics options](../get-started/linux.md#graphics-options).

### Linux, Intel graphics: the game freezes when it first goes into the Alps

The game's first-time intro hangs some Intel integrated GPUs (`journalctl -k | grep -i "gpu hang"` shows it). A profile
past the intro plays normally. To avoid it on a new PC or a new ReSteep folder, **import your progress before the
first Play** ([Moving to another PC](../play/progress.md#moving-to-another-pc)).

### The in-game menu doesn't open

- On Linux, check that **Settings → Linux → In-game menu** is on.
- If the game uses **N** for something else, choose another key under **Settings → General → Hotkeys**. **Home**
  opens the menu too.

## Saves and progress

- **The intro plays again.** Your save and your progress on the server no longer match: a new `data` folder (a new
  ReSteep folder or PC) gives you a new player without a save, and saves or progress changed by hand break the match.
  Use **Restore** or **Import progress**: [Progress and saves](../play/progress.md).
- **Ubisoft Connect says there was a problem getting your latest save.** The save files on your PC were replaced by
  hand. Use **Restore** instead of copying files.
- **A save no longer loads.** Restore a backup: [Backups](../play/progress.md#backups).

## Mods

- **A red line on a mod's tile, or ERROR on the in-game MODS page:** the mod has a problem, written next to it. It is
  not used until it is fixed; remove it or ask its author.
- **"Needs a file you download":** the mod is built once you have its file:
  [Mods that need a file you download](../mods/_index.md#mods-that-need-a-file-you-download).
- **"The mod build failed: …":** the reason is in the message and the logs. On Windows the game still starts.
- **Changes don't show:** new gear, textures and world changes need a game restart.
- **A mod doesn't react to your controller:** update ReSteep; mods now read the gamepad you are using, not Steam's
  virtual one.
- **Linux, "Open the ReSteep window for this":** on Linux the window keeps the mods. Open it (the game keeps
  running) and try again.
- **Linux, "This mod carries code …":** ReSteep only adds mods without native code or scripts from a file:
  [Mod safety](../mods/safety.md#native-code).
