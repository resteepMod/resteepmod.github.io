---
title: Logs and bug reports
weight: 10
---

# Logs and bug reports

## The quick way

**Settings → Setup & repair → Copy diagnostics** copies one report: versions, settings, what is set up, the start's
steps and the ends of the logs. It also saves it as `resteep-report-<time>.txt`. Email addresses are left out.
**Open logs** next to it opens the logs folder.

For an issue, **Save logs (zip)** puts that report and the logs themselves into one `resteep-logs-<time>.zip` and
opens its folder. Tickets, tokens, passwords, private keys, email addresses and your user name in folder paths are
replaced; server addresses stay.

> [!WARNING]
> Look through logs before you share them, and never post a password.

## Where the logs are

| | |
| --- | --- |
| **Windows** | `%LOCALAPPDATA%\ReSteep\data\launcher\logs`: `resteep-app.log` (the window), `server-console.log` (the server) and the diagnostics reports |
| **Linux, the window** | `~/.local/state/resteep/logs`: `resteep-window.log` and the diagnostics reports |
| **Linux, the session** | `$XDG_RUNTIME_DIR/powder-wrap.log` (the server and the session), and in the ReSteep folder `data/logs/launcher-session.log` (Wine and the game) and `data/logs/launcher-build.log` |
| **Linux, beside the game** | `powder_tls.log` (the TLS helper) and `powder_overlay.log` (the in-game menu), next to `Steep.exe` |

On Windows, `powder-cli.exe --status` in a command prompt in the program's folder prints what ReSteep has set up on
this PC.

## A good bug report

[Open an issue](https://github.com/resteepMod/ReSteep/issues) and say:

- what you did, what you expected and what happened;
- which system you play on (Windows or Linux) and which Steep (Steam or Ubisoft Connect);
- and attach the diagnostics report.
