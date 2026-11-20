---
title: Host a server
weight: 50
bookFlatSection: true
---

# Hosting a server

Every ReSteep already runs a server for its own player. Hosting means opening it to others, so friends can join with
their own accounts and progress.

## Hosting on Windows

1. On the launcher's **Server** page, switch on **Open to others**. It applies the next time the server starts.
2. Give your friends the address shown under **Reachability**, for example `192.168.1.20#3f9a0c...`.
3. On the next Play, ReSteep offers to add the firewall rules the other PCs need. They allow only the local network,
   on networks Windows treats as private.

On the same page you can set the server's **Name**, **Max players** and a **Password**, choose **Guest rights**, and
**Kick** or **Ban** players.

## Hosting on Linux

1. On the window's **Server** page, choose **This PC's server** and switch on **Open to others** (or *Open to other
   players* in the in-game menu's **This PC** page).
2. Choose the port (8443 by default). It needs no root: ports from 1024 up are open to normal programs.
3. If ufw or firewalld runs, let the port in once, as root. The page shows the command for yours, for example
   `sudo ufw allow 8443`. ReSteep never changes the system itself.
4. From the next Play (or at once: the window asks to restart Steep), others join with the address under
   **Others join with**, for example `192.168.0.181:8443#7ab8f6d5...`.

## Ports

A server needs **one port**, TCP and UDP of the same number: 443 by default, or the one you chose on Linux.

| Protocol | What |
| --- | --- |
| TCP | HTTPS for the game and Ubisoft Connect, and the certificate's revocation list |
| UDP | The game's online session (Quazal NEX) and the peer-to-peer helpers (Storm) |

The players' games also talk to each other directly over UDP. On a local network that needs nothing but the
firewall rule for Steep. A server behind a port forward that changes the number says so with `public_https_port` in
`config.toml`.

## Over the internet

Hosting over the internet works like on a local network, with the port forwarded to your PC.

> [!CAUTION]
> A server reachable from the internet should set `public = true` under `[server]` in `config.toml`. Without it, the
> server treats connections from its own PC as its owner. A loopback tunnel (playit, ngrok, frp, `ssh -R`) makes every
> guest look like that, so **always set `public = true` when you expose a server through a tunnel.**

## More

- [Accounts and players](accounts.md): who becomes which player, passwords, bringing your progress along.
- [Administration](admin.md): server commands, bans, the whitelist, the admin page.
- [News in Ubisoft Connect](news.md): your server's own news on Connect's start page.
- [The game-data pack](game-data.md): the store catalogue and achievements.
