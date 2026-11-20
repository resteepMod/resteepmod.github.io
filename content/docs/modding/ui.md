---
title: A mod's own UI
weight: 40
---

# A mod's own UI

A mod can have a **panel** on the MODS page (under its card) and **windows** over the game, drawn with the in-game
menu's own widgets. No native code is needed: the world editor's panel, free camera and tool window are all Lua.

## How it works

The mod lists its widgets every frame it wants them, like drawing:

- the panel's in a `panel` handler, which runs only while the panel shows;
- a window's inside `resteep.ui.window(title, fn)`, called from any other event (usually `frame`).

What the player did comes back in the next frame: a button returns `true` once, a value widget returns the new
value and `true`. Keep the value in a variable and pass it in again every frame:

```lua
local speed, near = 15, false

resteep.on("panel", function()
    local ui = resteep.ui
    ui.text("hello", "dim")
    speed = ui.slider("speed", speed, 1, 400, {format = "%.0f m/s", log = true})
    near = ui.checkbox("only near me", near)
    if ui.button("Go") then resteep.notify("go at " .. speed) end
end)
```

Labels are also the widgets' names: two widgets in one place need different labels. `"undo##12"` shows `undo` (the
part after `##` only tells them apart); `"##filter"` shows nothing.

## Widgets

| Call | Returns |
| --- | --- |
| `ui.text(text [, color])` | A line of text |
| `ui.button(label [, opts])` | `true` when clicked |
| `ui.checkbox(label, value)` | value, changed |
| `ui.slider(label, value, min, max [, opts])` | value, changed (`format`, `int`, `log`) |
| `ui.number(label, value [, opts])` | value, changed (`step`, `format`, `int`) |
| `ui.input(label, text [, opts])` | text, changed (`hint`, `max`) |
| `ui.combo(label, options, index)` | index, changed |
| `ui.list(label, items, selected [, opts])` | selected, changed (`height`, `columns`) |
| `ui.section(label, fn [, opts])` | A section that folds |
| `ui.scroll(label, lines, fn)` | A framed area that scrolls |
| `ui.same_line()` / `ui.separator()` | Layout |
| `ui.window(title, fn [, opts])` | A window over the game this frame |
| `ui.menu([open])` | Whether the menu is open; open or close it |

Colours: `"#RRGGBB"`, `"#AARRGGBB"`, or the menu's own `"dim"`, `"good"`, `"warn"`, `"bad"`, `"accent"`. Common options:
`disabled`, `width` (in font heights; -1 = the whole width), `color` (a button's fill).

Limits per mod and frame: 1500 widgets, 20000 list cells, 4 windows, nesting 8 deep.

## Taking over the mouse

A tool such as a free camera captures the input with `resteep.input.capture(true, "pointer")` every frame: the game
then gets no keyboard and mouse, while the mod's windows still take clicks. `resteep.input.pointer()` says where the
mouse is, and `resteep.input.mouse()` how far it moved.
