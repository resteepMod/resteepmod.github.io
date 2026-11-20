---
title: From the source code
weight: 40
---

# Running ReSteep from the source code

For developers and testers: you build everything yourself and update with `git pull`. Players should use the
releases ([Windows](windows.md), [Linux](linux.md)).

## What you need

| | Windows | Linux |
| --- | --- | --- |
| Source | `git clone https://github.com/resteepMod/ReSteep` | the same |
| Server | Rust from [rustup](https://rustup.rs) (the toolchain is pinned in `rust-toolchain.toml`) | the same |
| Launcher | [uv](https://docs.astral.sh/uv/) (it brings Python 3.12) | Python 3 with GTK 3 and WebKitGTK 4.1 (Arch: `python-gobject webkit2gtk-4.1`; Debian/Ubuntu: `python3-gi gir1.2-webkit2-4.1`) |
| Native parts | [zig](https://ziglang.org/) for the TLS helper | a MinGW-w64 cross compiler (`x86_64-w64-mingw32-gcc`/`g++`) |
| Other | | `unshare`, `ip`; `pasta` and `nft` to join or host; `python-zstandard` for content mods |

## Build and start

{{< tabs >}}
{{% tab "Windows" %}}
```
cargo build --release      # the server: target\release\powder-server
native\build.ps1           # the TLS helper, once
uv sync
ReSteep.cmd                # the launcher window
```
{{% /tab %}}
{{% tab "Linux" %}}
```
linux/powder-launcher                  # the window
linux/powder-launcher install-desktop  # add it to the application menu
```
The first start installs the window's Python parts (pinned and hash-checked) into `.venv-window`. The first Play
builds the server, the TLS helper and the in-game menu; **Settings → Setup & repair → Build ReSteep** does the same.
{{% /tab %}}
{{< /tabs >}}

From a checkout, files go to the checkout instead of `%LOCALAPPDATA%\ReSteep` or `~/.local/share/resteep`.

> [!WARNING]
> **On a PC you already played on, copy the old `data/` folder into a new checkout before the first Play.** The
> server's database there holds your player id. A fresh `data/` makes a new player, which has no save, so Steep
> starts the first-time intro again.

## Useful commands

```
cargo test && cargo clippy --all-targets   # the server's tests
uv run pytest                              # the launchers' and tools' tests
target/release/powder-server run           # the server alone (reads ./config.toml)
uv run powder --status                     # Windows: what the launcher has set up on this PC
uv run powder --restore                    # Windows: undo it
linux/powder-launcher launch --dry-run     # Linux: what a Play would run
```

Server commands are written as `powder-server ...` in these docs: that is `target/release/powder-server` in a
checkout and `powder-server.exe` in the installed Windows program. See [Server commands](../hosting/admin.md).
