# Security & privacy

## Where your data lives

Everything you type stays in your own browser's `localStorage`, on that one device.
There is no account, no server, no database, and no sync. The app makes **zero network
requests** after the page loads — no analytics, no fonts, no CDNs, no telemetry. Nobody,
including whoever hosts the page, can read your maps.

The practical consequence: clearing your browser's site data deletes your maps, and a map
made on your laptop will not appear on your phone. Use **File → Export JSON** to keep a
real backup, and **Import JSON** to move a map between devices.

## What was found and fixed

A review on 28 August 2026 tested the app against hostile input rather than only reading
the code. One real vulnerability was found and fixed.

**Stored XSS through an imported map file (fixed).** Node colours from an imported
`.json` were written straight into HTML attributes. A colour like
`#fff" onmouseover="…` closed the attribute and injected an event handler, so opening a
map file someone sent you could run their JavaScript — which could then read every saved
map and send it anywhere. Both injection points (the SVG branch lines and the map list)
were confirmed exploitable before the fix, and confirmed blocked after it.

Fixes applied:

- **Colour allowlist** — every colour that reaches an attribute or a style must match a
  plain hex literal (`safeColor`), anything else falls back to the default. Applied at
  render time, so a hostile value cannot reach the DOM by any route.
- **Import sanitiser** — imported and stored maps are rebuilt field by field with checked
  types (`sanitizeMap`), then the tree is regrown from the root. Cycles, self-parenting
  nodes, orphans, and `__proto__` / `constructor` keys are dropped rather than trusted.
  Text is capped at 2,000 characters per node, 5,000 nodes and 8 MB per file.
- **Content Security Policy** — `default-src 'none'` with `connect-src 'none'`, so even if
  something did execute, it has no way to send data out. No external scripts, styles,
  images, or frames can load.
- **No third-party requests** — the Google Fonts link was removed; the app now uses system
  fonts and loads nothing from outside its own origin.
- **Imports never overwrite** — an imported file always becomes a *new* map, so a bad file
  cannot destroy work you already have.
- **Storage is validated on read** — a map is sanitised when loaded, not only when
  imported, so tampered `localStorage` is handled the same way as a hostile file.
- **`spellcheck="false"`** on editable text, so note contents are never sent to a
  browser vendor's spell-check service.
- **`referrer: no-referrer`** — the page leaks no URL information if a link is ever added.

## What is deliberately not protected

- **Anyone with access to your unlocked device** can open the browser and read your maps.
  This is a local notepad, not a vault — do not keep passwords or secrets in it.
- **Clickjacking** — `frame-ancestors` only works as an HTTP header, and GitHub Pages
  cannot set headers. On a host that can (Netlify or Cloudflare Pages, via a `_headers`
  file) add `X-Frame-Options: DENY`.
- **A malicious host** could serve modified JavaScript. You control the repo, so this
  means: keep your GitHub account secure with 2FA.

## Reviewing it yourself

The whole app is one readable file. To confirm the claims above:

```bash
grep -nE "fetch\(|XMLHttpRequest|WebSocket|sendBeacon|https?://" index.html
```

That returns nothing outside comments — there is no code capable of sending your data
anywhere.
