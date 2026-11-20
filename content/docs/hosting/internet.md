---
title: Over the internet
weight: 5
---

# Sharing your server over the internet

**Open to others** lets PCs on your own network join. To play with friends somewhere else, you also share the server
over the internet: your router passes one port on to your PC, and ReSteep shows the address your friends join with.

## What you need

- **A router you can set up.** You add one port forward on it (below).
- **A public IPv4 address.** Most home connections have one. Some providers put many customers behind one address
  (carrier-grade NAT, CGNAT); then a port forward can't work. Signs of it: the internet address ReSteep shows differs
  from the address your router's status page shows, or the router's address starts with `100.64` to `100.127`. Ask
  your provider for a public IPv4 address, or use a [VPN instead](#with-a-vpn-instead).
- **Your own copy of Steep.** Run [Check my add-ons](../get-started/dlc.md) once with the Ubisoft account that
  owns Steep (Steam or Ubisoft Connect). Until a check found it, ReSteep keeps your server on your own network and
  the Server page says so.
- **One port, TCP and UDP:** the **Port** on the Server page (443 by default on Windows, 8443 on Linux).

## Set it up

1. In ReSteep, open **Server** and switch on **Open to others**, then **Share over the internet**.
2. **Set a password** on the same page (Windows: **Password**; Linux: while the server runs). Without one, anyone who
   finds your address can make an account and play.
3. **Forward the port on your router.** The Server page says which port and to which address, for example "forward port
   443 (TCP and UDP) to this PC (192.168.1.20)". On the router's page this is usually under *Port forwarding*,
   *Virtual server* or *NAT*. Forward **both TCP and UDP**, and nothing else. Give your PC a fixed address in your
   network (the router's *DHCP reservation*), so the forward still points at it tomorrow.
4. **Linux:** if ufw or firewalld runs, let the port in once; the Server page shows the command. On Windows, Play
   offers the firewall rule itself.
5. Press **Play** (or start the server again). Give your friends the address under **Over the internet**, for example
   `203.0.113.7#3f9a0c11…`. They add it in their ReSteep like any other server
   ([Playing with friends](../play/multiplayer.md)), and type your server password the first time.

Friends on your own network keep using the address under *Reachability*: most routers don't loop their own internet
address back inside.

ReSteep finds your internet address by asking a public "what is my IP" service (api.ipify.org, else Cloudflare's)
while sharing is on. That request carries nothing about you. If your provider changes your address, ReSteep finds the
new one at the next start; give your friends the new address.

## Private or Public

Under **Who can find it**:

- **Private** (the default): only players you give the address to can join.
- **Public:** your server also appears in ReSteep's community server list, with its name, how many play, its mods and
  whether it has a password. Anyone can see it there and try to join.

The community list is curated: to be listed, ask its admins (on ReSteep's Discord) for a **listing id and token** and
paste them into the Server page. ReSteep keeps them protected on your PC and gives them only to your own server. Your
server is listed while it runs and drops off the list a few minutes after it stops.

## What it means for security

Sharing over the internet opens one door into your PC. Here is what goes through it, and what doesn't.

**What is reachable.** Only the ReSteep server, on that one port. The port forward and the Windows firewall rule name
that port and that program only; nothing else on your PC becomes reachable. The Windows rule still applies only on
networks Windows treats as private.

**Your address.** Everyone you give the address to, and everyone who sees your server in the list when it is Public,
learns your internet address. It tells roughly where you are and who your provider is. Share it with people you know;
choose Public only if you are fine with strangers seeing it. Steep's multiplayer also connects the players' games
directly to each other, so players in a session see each other's addresses, as they did on Ubisoft's servers.

**Who gets in.** With a server password, a PC that hasn't given it can't make an account, sign in or play. Wrong
guesses are rate-limited. Without a password, anyone with the address can make an account and play (but never as you
or as another player). You can kick and ban players, ban addresses, or let in only a whitelist:
[Administration](admin.md).

**Accounts.** Each player has their own account on your server, with a password stored only as a hash. These are not
Ubisoft accounts, and your players' Ubisoft passwords never reach your server. Shared over the internet, the server
also accepts only sign-in tickets it issued itself.

**Your own powers stay yours.** Host settings and the admin tools work only from your own PC. A guest from the internet
is never taken for you.

**Keep it running only when you play.** The server runs while ReSteep plays (Linux) or while the window is open
(Windows). Keep ReSteep up to date: it is the program strangers can reach.

> [!CAUTION]
> Use a port forward or a VPN, not a TCP tunnel service (playit.gg, ngrok, frp, `ssh -R`). A tunnel makes every guest
> look like your own PC, which a ReSteep server treats as its host. If you must use one, set `public = true` under
> `[server]` in `config.toml`; your own Ubisoft Connect then no longer signs in by itself.

## With a VPN instead

If you can't forward a port (CGNAT, a router you don't control), a VPN such as Tailscale or ZeroTier puts your friends'
PCs into one private network with yours. Leave **Share over the internet** off: with **Open to others**, your friends
join with your PC's VPN address. Nothing is open to the internet then.

## If friends can't connect

- Check that the forward covers **TCP and UDP** and points at your PC's current address.
- Try the address yourself from outside your network, for example from a phone on mobile data with a friend's help.
- Look for CGNAT (above).
- Some providers block incoming port 443. Choose another **Port** on the Server page (from 1024 up), forward that
  one instead, and give friends the new address: ReSteep adds the port to it. If the server runs, ReSteep offers to
  restart it on the new port (or, while you play, uses it from the next Play).
- A friend who sees "This server needs its server password" types the password you gave them; a changed password is
  asked again at their next Play.
