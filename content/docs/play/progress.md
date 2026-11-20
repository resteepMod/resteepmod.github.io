---
title: Progress and saves
weight: 40
---

# Progress and saves

Your progress lives in two places that must agree: **the server's profile** (level, credits, gear, medals, stats)
and **the game's save files** on your PC. Steep checks the save against the server. When the two no longer match,
the first-time intro comes back.

> [!WARNING]
> Never edit levels or unlocks by hand, and never copy old save files back by hand. Use the tools below: they keep
> both parts together.

## Backups

**Settings → Setup & repair** keeps:

- **Automatic backups** of your profile and save files, made before every Play and before every restore;
- **Manual backups**, made with **Back up now**.

To go back: close Steep, pick a backup and press **Restore**. How things are now is backed up first, so you can
undo a restore.

## Moving to another PC

Under **Settings → Setup & repair → Your progress** (Steep closed; on Windows the local server stopped):

- **Export progress…** writes one `.zip` with everything that makes you who you are: the server's profile, the
  cloud copy of your save, your save files, and the game's settings with its copy of the item list. Each PC keeps its
  own server certificate.
- **Import progress…** on the other PC puts that file in place. Your progress there is backed up first.

> [!TIP]
> Import **before the first Play** on a new PC or a new ReSteep folder. A new, empty `data` folder makes the server
> give you a new player, which has no save, so the intro plays again.

## Starting over

**Reset progress…** starts over: the server's progress and the save files together, so the intro plays at the next
Play. It asks twice and makes a backup first ("before the reset"), which brings everything back.

## Cloud saves

Ubisoft Connect uploads the game's save files to the server when you quit, and gets them back when you start on
another PC. This also works between the Steam and the Ubisoft Connect version.

If Connect says there was a problem getting your latest save, the save files on your PC were probably replaced by
hand. Use **Restore** instead of copying files: it restores both parts together.

## Your progress from Ubisoft's servers

A host can import progress once from recordings of their own online sessions (`powder-server admin import`):
[Accounts and players](../hosting/accounts.md#bringing-your-progress-along). Players can't make such recordings
themselves.
