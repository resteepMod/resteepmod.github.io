---
title: Your first mod
weight: 10
---

# Your first mod

A script mod that says how long you were in the air after every big jump.

## 1. Make the folder

Open the mods folder (in the launcher, **Mods → Open mods folder**) and make a folder `airtime-note` with one file,
`main.lua`:

```lua
resteep.on("landing", function(airtime)
    if airtime > 2 then
        resteep.notify(string.format("%.1f s in the air!", airtime), 2)
    end
end)
```

That is a complete mod. With a ReSteep checkout you can let the tools set up a mod in the full layout instead:

```
python -m resteep new airtime-note
```

It writes the manifests, an icon and a `.luarc.json` for your editor.

## 2. Run it

Start the game, press **N** and open **MODS**. Your mod is listed; switch it on. Jump off something: after more than
two seconds in the air, a note appears.

A mod reloads by itself when its `main.lua` changes, so you can edit it while the game runs. If it has an error,
the MODS page shows **ERROR** and the reason in red, and the other mods go on.

## 3. Try calls in the console

The MODS page's **CONSOLE** has a Lua line under the log. Type a call and press Enter:

```lua
resteep.player()
```

The result shows in the log. A variable you set stays for the next line. Handlers and timers set in the console
don't run: write a mod for those.

## 4. Get completion in your editor

VS Code with the Lua extension (LuaLS) completes `resteep.` and checks your arguments when you open the mods folder:
its `.luarc.json` points LuaLS at ReSteep's API annotations. For a mod elsewhere, add `native/sdk/resteep.lua` from
the ReSteep repository to LuaLS's `workspace.library`.

## Next

- Save data between sessions with `resteep.save` / `resteep.load`, and send scores to a leaderboard:
  [Saving and the server](lua-api.md#saving-and-the-server).
- Give it settings players can change: [Settings](format.md#settings).
- Give it a panel: [A mod's own UI](ui.md).
- Share it: [Publishing](publishing.md).
