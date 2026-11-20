---
title: Playing with friends
weight: 30
---

# Playing with friends

Every ReSteep runs a server. One of you **hosts** (opens their server to others) and the others **join** it.
Windows and Linux players can play together: either can host, either can join.

## Join a friend's server

Your friend's ReSteep shows an address to give out, for example `192.168.1.20#3f9a0c...` or, for a Linux host,
`192.168.1.20:8443#3f9a0c...`. The part after `#` is the start of their server's certificate fingerprint: with it,
ReSteep checks that it reached their server and not someone in between.

{{< tabs >}}
{{% tab "Windows" %}}
1. Press **Play** to start the game.
2. Open the in-game menu (**N**), go to **Server**, add the address under **SERVERS** and press **JOIN**.
{{% /tab %}}
{{% tab "Linux" %}}
1. In the ReSteep window, open **Server**, add the address under **Add a server** and press **Choose**.
2. Press **Play**. **This PC's server** takes you back to your own.
{{% /tab %}}
{{< /tabs >}}

The first time, ReSteep shows the server's certificate fingerprint and asks **Trust this server**. Compare it with
your friend's if you can. If a server you trusted later shows a *different* certificate, Play stops with a warning:
either your friend made a new one, or someone is listening in. Ask before you continue.

## Your account on a server

The first time you play on a server, ReSteep asks for your account there:

- **Create an account**: a player name, an email and a password. You start as a new player on that server.
- **I have one**: sign in with an account you already made on that server, from another PC for example.

> [!IMPORTANT]
> **This is not a Ubisoft account.** It exists only on that ReSteep server, and Ubisoft never sees it. The email is
> only your sign-in name there; no mail is sent to it. Don't reuse your real Ubisoft password.

If the server has a password, the same window asks for it: the host gives it to you. ReSteep keeps it for that server
and gives it again at every Play; if the host changes it, you are asked again.

ReSteep keeps the account for that server and uses it from then on. Ubisoft Connect signs in with it by itself. If
Connect asks anyway, type that email and password. If the host makes a new certificate, the server counts as a new
one and you are asked again.

## Mods on a server

When you join, ReSteep shows which mods the server runs:

- mods **everyone needs** (new items, maps, challenges), marked **YOU DON'T HAVE IT** or **YOURS IS DIFFERENT** where
  yours differ;
- optional looks and scripts;
- mods only the server runs.

With different shared mods, places and items may not match what the others see; you can still **JOIN ANYWAY**. A
server never installs anything on your PC. Which official mods must match: [Official mods](../mods/official-mods.md).

## Switching servers while you play

- **Windows:** the game moves to the other server without a restart.
- **Linux:** switching restarts Steep, because the game's network is set up when it starts. ReSteep asks *Restart
  Steep?* first; **Later** keeps the choice for the next Play. Unsaved progress in the current run is lost. The
  ReSteep window has to be open, since it starts the game again.

A server with a password asks for it before you switch.

## What works together

On a server, riders in the same area meet. Form a group by pressing **G** next to each other, or **Join group** in
the social tab; spectating works too. Every other player on the server is your friend in the game. Leaderboards,
shared rides, photos and player-made challenges are the server's: see [What works](features.md).

To host for others, see [Hosting](../hosting/); for friends outside your network,
[Over the internet](../hosting/internet.md).
