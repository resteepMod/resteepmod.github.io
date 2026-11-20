---
title: Files and settings
weight: 30
---

# Files and settings

## Where ReSteep keeps what

| | Windows | Linux |
| --- | --- | --- |
| The program | `C:\Program Files\ReSteep` or `%LOCALAPPDATA%\Programs\ReSteep` | the AppImage you downloaded |
| Your data, settings and mods | `%LOCALAPPDATA%\ReSteep` | `~/.local/share/resteep` |
| The window's logs | `%LOCALAPPDATA%\ReSteep\data\launcher\logs` | `~/.local/state/resteep/logs` |

From the source code, the checkout itself holds the data.

## Inside the data folder

| Path | What |
| --- | --- |
| `config.toml` | The server's settings (optional; see `config.example.toml` in the repository) |
| `mods/` | Your mods |
| `modconfig/` | The mods' settings, and approvals of native code |
| `gamedata/` | The game-data pack |
| `data/powder.db` | Players, accounts, progress, bans and the whitelist |
| `data/tls/` | The server's certificate authority and certificate |
| `data/cloudsaves/` | Cloud saves |
| `data/news.json`, `data/news/` | [News in Ubisoft Connect](../hosting/news.md) |
| `data/launcher/` | The launcher's settings, pinned servers, your accounts on other servers |
| `data/logs/` | The server's and the session's logs |

> [!IMPORTANT]
> `data/` is who you are to the server. Take it along (or use **Export progress**) when you move to a new PC or a new
> ReSteep folder, or you start as a new player.

## The server's config

The most used settings in `config.toml`:

```toml
[server]
name = "My server"
motd = "Welcome!"
public = false            # true for a server reachable from the internet
admins = ["<profile id>"]
# public_https_port = 0   # when a port forward changes the port number

[players]
# registration = "open"   # "closed": only the host creates accounts

[mods]
enabled = ["*"]           # which server mods run: names, or "*" for all
```

## Linux session settings

`powder-wrap` runs one session; the window sets these for you. Started by hand, it reads them from the environment:

| Variable | What |
| --- | --- |
| `POWDER_CONFIG` | The server's config |
| `POWDER_WINE` | The Wine the prefix runs with |
| `POWDER_OVERLAY=1` | The in-game menu |
| `POWDER_CLIENT_MODS=name,name` | The mods to load for the session |
| `POWDER_JOIN=address[#fingerprint]` | Play on a server on another PC |
| `POWDER_TLS_DELAY_MS=20000` | A fixed delay for the TLS helper ([Troubleshooting](../troubleshooting/_index.md#linux-steep-closes-a-few-seconds-after-it-starts)) |

The session's output goes to `$XDG_RUNTIME_DIR/powder-wrap.log`.
