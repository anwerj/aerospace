# AeroSpace preferences

Config file: `~/.config/aerospace/aerospace.toml`

AeroSpace loads this path, or `~/.aerospace.toml`. A leading dot on the filename (`~/.config/aerospace/.aerospace.toml`) is ignored and the built-in default config is used instead. Keep the name `aerospace.toml`.

Check behavior against https://nikitabobko.github.io/AeroSpace/guide#configuring-aerospace before changing commands. After edits, `aerospace reload-config`.

## Hardware

This config is shared by two laptops, work and personal. Each setup is one external monitor plus the laptop display. Monitor model names differ. Do not hardcode a name such as CB272K, and do not assign workspaces by left-to-right sequence number.

The external monitor is the macOS main display (System Settings → Displays → Use as). The laptop panel is the built-in display. AeroSpace patterns: workspace 1 = `main`, workspace 2 = `built-in`.

## Layout

- Exactly two workspaces, one per monitor. Do not add a third.
- `config-version = 2`, so empty workspaces disappear unless listed. Keep `persistent-workspaces = ['1', '2']`.
- `workspace-to-monitor-force-assignment`: workspace 1 = `main` (external), workspace 2 = `built-in` (laptop).
- Root layout is `accordion`. Both monitors are wide, so the root is a horizontal accordion.
- Windows stay in one horizontal row. No vertical splits, no stacked containers, no up/down movement inside a workspace.
- All gaps stay 0.
- Start AeroSpace at login.
- When the focused monitor changes, move the cursor to that monitor's center with `on-focused-monitor-changed = ['move-mouse monitor-lazy-center']`. This includes Command-Tab onto the other display. Do not use `on-focus-changed` for this. Left and right focus on the same screen must not move the cursor.

## Keys

WASD. Do not switch this to hjkl.

| Key | Action |
|---|---|
| `alt-a` / `alt-d` | Focus left / right |
| `alt-shift-a` / `alt-shift-d` | Move the window left / right |
| `alt-w` / `alt-s` | Focus the next / previous monitor |
| `alt-shift-w` / `alt-shift-s` | Move the window to the next / previous monitor and follow it |
| `alt-1` / `alt-2` | Jump to the main (external) display / the built-in laptop display |
| `alt-shift-1` / `alt-shift-2` | Send the window there and follow it |

Monitor movement uses `focus-monitor` and `move-node-to-monitor` with `--wrap-around` and `next` / `prev`. With two monitors, either key lands on the other display.

`alt-1` and `alt-2` stay. Changing monitor keys must not remove the other bindings.

## Do not

- Do not bind focus or move up/down inside a workspace (`alt-j`, `alt-k`, `focus up`, `focus down`, `move up`, `move down`). Splits are not used.
- Do not bind `alt-w` / `alt-s` to `focus-monitor up` / `down`. That was tried and rejected. Display arrangement is not the same on both laptops, and up/down is not the binding.
- Do not use `workspace next` or `workspace prev` to change monitors. Those commands only cycle workspaces on the monitor that is already focused, and each monitor has one workspace, so the key does nothing. On AeroSpace 0.21 they also require `--stdin` or `--no-stdin`.
- Do not replace this config with the old three-workspace setup (two workspaces on the external monitor, a third on the laptop, `alt-j` / `alt-k` only).
- Do not name a specific external monitor model in the config or in this file.
- Do not drop bindings while editing one of them.
