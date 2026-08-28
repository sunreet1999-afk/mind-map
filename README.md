# Mindly — a mind map you build yourself

Open `index.html` in any modern browser. That's it — no install, no server, no account.

## Making a map
- **Tab** — add a child to the selected node
- **Enter** — add a sibling
- **F2** or double-click — rename
- **Delete** — remove the node and its branch
- **Space** — collapse / expand a branch
- **Arrow keys** — move the selection around
- Hover a node and click **+** to add a child with the mouse
- **Drag a node onto another** to re-parent it
- Click a colour swatch at the bottom to recolour a branch

## Several maps at once
**Maps** in the toolbar lists everything you've made. Click a map to open it, use
**New mind map** to start another, or **Duplicate this map** to branch off a copy.
A map is named by its centre node, so renaming the centre renames the map. The x on
a row deletes it. Everything switches instantly and saves on its own.

## Canvas
- Drag empty space to pan, scroll to pan, **Ctrl/⌘ + scroll** (or pinch) to zoom
- **F** fits the whole map on screen, **Ctrl+0** resets zoom
- **Ctrl+L** re-tidies the layout, **Ctrl+Z / Ctrl+Shift+Z** undo and redo

## Saving
The map saves itself to this browser automatically. Use **File → Export JSON** for a real
backup (and **Import JSON** to bring it back), or **Export PNG** for a shareable image.

## On a phone
The layout switches to a touch build under 760px wide: a bottom action bar
(Child / Next / Rename / Fold / Delete), always-visible + handles, one-finger pan,
pinch to zoom, and tap-a-selected-node-again to rename. Hosted over https it also
installs to the home screen as a fullscreen app — see HOSTING.md.

## Putting it online
See [HOSTING.md](HOSTING.md) — Netlify Drop takes about a minute, GitHub Pages about ten.

## Files
- `index.html` — the entire app (markup, styles, logic)
- `manifest.json`, `icon.svg`, `icon-maskable.svg` — home-screen install support
- `.claude/launch.json` — optional dev-server config for previewing over http
