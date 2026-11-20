---
title: Rules and legal stance
weight: 10
---

# Rules and legal stance

> [!IMPORTANT]
> **Draft.** This page states the project's intended stance and the rules for shared mods. Some of the checks it
> describes are still being built.

## What ReSteep is

ReSteep is an unofficial, community-run fan project. Steep is a game by Ubisoft that needs Ubisoft's online services
for its progression, challenges and rewards. Those services still run today, but not forever. ReSteep is a
replacement for them that players choose to use, so that copies people own stay playable, also once Ubisoft's servers
are switched off, and it adds a modding platform. It doesn't change Ubisoft's servers.

ReSteep is not affiliated with, endorsed by or supported by Ubisoft or Valve. Steep and Ubisoft Connect are
trademarks of Ubisoft.

**ReSteep is not a crack, and not a way to play Steep without owning it.** It starts your own installed copy through
Steam or Ubisoft Connect and points it at a ReSteep server instead of Ubisoft's.

## Owning the game is required

You need your own, legitimately bought copy of Steep (Steam or Ubisoft Connect). ReSteep doesn't provide the game.

## No game data is shipped

- ReSteep's repository and releases contain no game files and no data from Ubisoft's servers.
- The optional game-data pack is not part of ReSteep.
- Mods carry only their own files. What a mod needs from the game is generated on the player's PC, from the player's
  own install.

## Paid content stays paid

ReSteep unlocks the base game, and gives paid add-ons (DLCs, the season pass's content, paid cosmetic packs) only to
players whose Ubisoft account owns them ([Your DLCs](../get-started/dlc.md)).

A mod may add new items of its own and give those to players. A mod must not grant, unlock or make free the game's
paid content: DLC packs and the season pass, Ubisoft Store or Ubisoft Club rewards, or real-money currency.

A server's store offers the base game's gear to everyone and a DLC's gear only to players who own that DLC; it never
lists paid gear for 0 credits. Older limited-time items (season, holiday and partner events, free to earn while they
ran) are not paid content: the store sells them to everyone. Gear the game hands out for playing (medals, missions,
levels, places found) is earned in the game, not sold.

## Code in mods

- **Shared mods hold data and sandboxed Lua only.** No executables or scripts that run outside the Lua sandbox.
- **Native code comes only from ReSteep itself**, built and shipped in ReSteep's own releases.
- Third-party native code is possible only outside shared mod listings: added by the player by hand, approved by the
  player, pinned to the exact files' hashes, with a warning.
- **A server can never push code to a player's game**, and can't approve code for a player.

## Rules for sharing mods

These rules apply to mods shared through ReSteep's channels, including a Steep community on Thunderstore once it
exists:

1. No mods that unlock paid content.
2. No packages with executables or scripts outside the Lua sandbox.
3. No game files, or data taken from the game, in a package.

ReSteep's mod checks refuse packages that break rules 1 and 2 where they can tell.

## No warranty

ReSteep comes with no warranty, to the extent permitted by law. Running a replacement server, redirecting Ubisoft's
hostnames, attaching code to the game or modding it may breach the terms of service or licence agreements of Ubisoft,
Steam or others. Whether it does, and what follows from that, depends on those terms and on where you live; this page
makes no legal claim either way.

The authors and contributors are **not responsible** for any consequences of using ReSteep, including bans or
suspensions of Ubisoft, Steam or other accounts, lost or corrupted progress or saves, data loss, or damage to your
system. Back up what matters to you.
