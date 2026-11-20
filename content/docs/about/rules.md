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

## Ubisoft's terms

Ubisoft's [Terms of Use](https://www.ubisoft.com/legal/documents/termsofuse/en-US) (January 2026) and the licence
agreement for its games ([EULA](https://www.ubisoft.com/legal/documents/eula/en-US), January 2023) forbid much of what
ReSteep does. Among other things, they forbid:

- creating, providing or using unauthorised private servers, server emulators and alternative launchers, and getting
  around security checks or copy protection (Terms 7.3.5, EULA 1.3);
- reverse engineering, decompiling or changing the game (EULA 1.2);
- trainers, scripts and other cheat programs, in single-player too (EULA 1.2, Terms 7.3.4);
- capturing the game's network traffic (Terms 7.3.6).

They also say that Ubisoft owns what is made from its games' content (Terms 10.1), and that Ubisoft can suspend or
close an account for breaking them, also for what its owner does outside Ubisoft's services (Terms 7.5, 8.2). The
game's anti-cheat may tell Ubisoft about programs it finds in the game's memory (EULA 4).

**What that means for you.** You use ReSteep at the risk of your Ubisoft account, and a closed account loses every
game on it, not only Steep. Where you live may limit what such terms can forbid and how they are enforced (consumer
law, the right to make programs work with each other). This page makes no legal claim either way.

**What ReSteep does about it:**

- **It stays apart from Ubisoft's services.** In a ReSteep session, Steep and Ubisoft Connect sign in to a ReSteep
  server, not to Ubisoft. ReSteep's in-game menu and hooks load only in a ReSteep session: on Windows the launcher
  attaches them when it starts the game, and on Linux its helper does nothing outside a session. When you start Steep
  through Ubisoft Connect or Steam, none of ReSteep's code runs in it.
- **It needs a copy you own.** ReSteep starts your installed game. Paid add-ons unlock only for their owners, and a
  server is shared over the internet only once a check found Steep on the host's Ubisoft account.
- **The add-on check** runs Ubisoft Connect on its own, without ReSteep, and only reads which Steep products your
  account owns.
- **No game data** in ReSteep or in shared mods (above).
- **Nothing is sold.** ReSteep is free. Don't sell access to a server, accounts, mods, or anything made from the game.

## No warranty

ReSteep comes with no warranty, to the extent permitted by law. Running a replacement server, redirecting Ubisoft's
hostnames, attaching code to the game or modding it may breach the terms of service or licence agreements of Ubisoft,
Steam or others. Whether it does, and what follows from that, depends on those terms and on where you live; this page
makes no legal claim either way.

The authors and contributors are **not responsible** for any consequences of using ReSteep, including bans or
suspensions of Ubisoft, Steam or other accounts, lost or corrupted progress or saves, data loss, or damage to your
system. Back up what matters to you.
