---
title: Security
weight: 20
---

# Security

## Reporting a vulnerability

Please **don't open a public issue**. Use GitHub's private reporting: the ReSteep repository's **Security** tab →
**Report a vulnerability**. Say what is affected (server, launcher, in-game menu, a mod, the installer or updater),
the version or commit, how to reproduce it, and what an attacker gains. The maintainers answer within a week, agree a
date before anything is published, and credit you unless you prefer not.

Supported: the newest release and `main`. The updater moves players forward.

## What protects players

- **A server can never put code on your PC.** Native mods load only after you approved exactly those files, pinned to
  their hashes; Lua and content mods are sandboxed or data.
- **Talking to the right server.** Each server's certificate authority is pinned on first use (or from the start, by
  the `#fingerprint` in its address) and never silently replaced. Inside the game, the TLS helper pins the server's
  own certificate.
- **Your other websites.** A server's certificate authority can only vouch for Ubisoft's names, checked before
  anything trusts it.
- **Your identity.** ReSteep's own credentials go to your own server only. Every other server gets an account of its
  own (the one you made there, or a password derived for that server alone), so no host can sign in as you elsewhere.
- **Your progress.** A player can change only their own data.
- **Updates.** Installed only with a checksum from the release, never older versions.

## What protects hosts

- **Accounts.** Passwords are stored as scrypt hashes and never logged; sign-ins are rate-limited.
- **The server process.** Size, connection and time limits on every protocol.
- **Who may play.** A server password (without it, a guest can't make an account or sign in), closed registration, a
  player limit, bans, the whitelist and kicks. Shared over the internet, the server accepts only tickets it issued.
- **The host's powers.** Host settings and admin actions only from the server's own PC, with a token only the
  launcher that runs the server can read.
- **The PC.** Server mods run in a Lua sandbox with memory and time limits.

Sharing over the internet, step by step and what it exposes: [Over the internet](../hosting/internet.md).

> [!CAUTION]
> **Don't expose a server through a TCP tunnel that forwards to 127.0.0.1** (playit.gg, ngrok, frp, `ssh -R`) unless
> `public = true` is set under `[server]`. Guests then arrive from loopback, which would otherwise count as the host's
> own PC. Prefer port forwarding or a VPN.

## Not protected, by design

- The owner of the server's PC can do everything, and a host can read and change everything their server stores.
- A program running as the same user can read the player's key and credentials.
- Approving a client mod trusts its host with your PC.
