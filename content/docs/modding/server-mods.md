---
title: Server mods
weight: 60
---

# Server mods

A server mod is Lua that runs on the server: `mod.lua` in the mod's folder (or `mods/<name>.lua`), returning a
function that receives the server's API. Use it for a mod's server half, leaderboards of your own, admin tools, or
to change what the server answers.

```lua
-- mods/welcome/mod.lua
return function(api)
    api.on("login", function(s) api.log.info(s.name .. " signed in") end)
end
```

## The API

| Call | What |
| --- | --- |
| `api.on(event, fn)` | Events: `login`, `nex_connected`, `purchase`, ... |
| `api.before_http(method, path_glob, fn)` | Answer an HTTPS request yourself; return `nil` to let the server answer |
| `api.before_rmc(method, fn)` | The same for the game's online-session calls |
| `api.save(key, value)` / `api.load(key)` | Keep data in the server's database |
| `api.log.info(...)`, `api.config` | Logging and the server's config |
| `api.settings` | The mod's own `[mods.settings.<mod>]` table of `config.toml` (read-only) |

## Requests and who sent them

An HTTP hook's request has `method`, `path`, `query`, `headers`, `body` and `peer`, and, when it carries a session the
server issued, `req.player = {profile_id, name, admin}`.

> [!IMPORTANT]
> Use `req.player` to decide who may do what, never `peer` (the address). `req.player` is verified by the server; the
> session ticket itself is never shown to a mod.

`req.own_pc` says the request comes from the server's own PC. `req.host_launcher` is set only when it also carries
the host token of the launcher running the server (the host's own in-game menu).

A mod's in-game script reaches its server half with `resteep.http(method, "/_powder/<mod id>/...")`; the mod answers
with `api.before_http` on that path.

## Limits

Server mods run with the host's trust, but as a safety net against bugs they get a reduced Lua library (`string`,
`table`, `math`, `utf8`, `coroutine`, `os.time`/`clock`/`date`; no `io`, `os.execute`, `require` or `debug`), share at
most 128 MB, and a hook that runs longer than 100 ms is aborted. Errors are logged and never reach the game.

## Running them

`[mods]` in the server's `config.toml` picks which mods run; names starting with `_` are skipped. List mods by name
rather than `"*"` for mods you install. `powder-server mods` loads them and shows what they hook.

The `admin` mod in the ReSteep repository, the server's [admin page](../hosting/admin.md#the-admin-page), is a
complete example.
