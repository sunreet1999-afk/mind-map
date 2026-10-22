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

## Notebook — dump notes, get a map
Click **Notebook** (or **Ctrl+B**) and just write, one thought per line. With **Live** on
the map rebuilds as you type; otherwise press **Build map** or **Ctrl+Enter**. Every map
keeps its own notebook, and a rebuild can be undone with **Ctrl+Z**.

How the text is read:
- **A paragraph** (mostly long lines, no bullets) → the most repeated word or pair of words
  becomes the centre, sentences that share a keyword are grouped under it, and long
  sentences split at commas and words like *because / but / lekin / kyunki*. Several
  paragraphs each become a branch named after their own main words. A short title line
  above the paragraph is used as the centre instead. For the smartest grouping, use
  **Build with AI**.
- First short line followed by a blank line → the centre (or a single `# Heading`)
- `## Headings` → main branches
- A line ending in `:`, or a plain line followed by bullets → holds the lines under it
- Indentation (spaces or Tab) → deeper levels; `-`, `*`, `•`, `1.` bullets are stripped
- `Topic: a, b, c` → a *Topic* node with three children; repeated topics merge
- `#tag` anywhere in a line → that line is grouped under a `#tag` branch
- A blank line closes the current group; very long paragraphs are split into sentences

Rebuilding replaces the map's structure with what the notes say, so hand-made edits to
nodes will be overwritten on the next rebuild. Colours and folded branches are kept.
**Build map** happens entirely in the browser: nothing is sent anywhere.

### Build with AI (optional)
For really messy dumps, click **AI** in the notebook, paste an Anthropic API key (from
[console.anthropic.com](https://console.anthropic.com)) and press **Build with AI**.
Claude (Opus 5) groups your notes by meaning, picks the branch names and a title, and keeps
your language — Hinglish stays Hinglish. It won't add ideas that aren't in your notes.

- Each press is one paid API request; the notes and key go only to `api.anthropic.com`.
- **Remember key on this device** saves the key in this browser — leave it off on a shared machine.
- Live is switched off afterwards so typing doesn't undo Claude's grouping; **Ctrl+Z** undoes it.
- Serve the folder over http (see HOSTING.md) — some browsers block API calls from a `file://` page.

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

## Security & privacy
No accounts, no server — maps live only in your browser. The one exception is the optional
**Build with AI** button, which sends that notebook to Anthropic's API when you press it.
Imported files are sanitised and the page runs under a strict Content Security Policy.
Details, including a fixed XSS issue, are in [SECURITY.md](SECURITY.md).

## Files
- `index.html` — the entire app (markup, styles, logic)
- `manifest.json`, `icon.svg`, `icon-maskable.svg` — home-screen install support
- `SECURITY.md`, `HOSTING.md` — security review and hosting steps
- `.claude/launch.json` — optional dev-server config for previewing over http
