# Hosting Mindly

Mindly is a plain static site — three files and two icons, no build step, no backend,
no database. Anything that serves static files will run it. Pick one:

| Option | Time | Cost | Good for |
| --- | --- | --- | --- |
| Netlify Drop | ~1 min | Free | Fastest way to get a public link |
| GitHub Pages | ~10 min | Free | A permanent home you can update by pushing |
| Cloudflare Pages | ~5 min | Free | Fast globally, free custom domain support |
| Local network | ~1 min | Free | Testing on your phone before publishing |

Whatever you choose, upload the **whole folder** — `index.html`, `manifest.json`,
`icon.svg`, and `icon-maskable.svg`. The `artifact/` folder is not needed.

---

## 1. Netlify Drop — the fastest

1. Go to https://app.netlify.com/drop
2. Drag the `mind map` folder onto the page.
3. You get a live URL like `https://random-name-123.netlify.app` in a few seconds.
4. Optional: sign in (free) to rename the site and keep it permanently.

To update later, drag the folder again.

---

## 2. GitHub Pages — a permanent home

Needs a free GitHub account and Git installed.

```bash
cd "D:/mind map"
git init
git add index.html manifest.json icon.svg icon-maskable.svg README.md HOSTING.md
git commit -m "Mindly mind map app"
git branch -M main
```

Create an empty repository on github.com (no README), then:

```bash
git remote add origin https://github.com/YOUR-USERNAME/mindly.git
git push -u origin main
```

In the repo: **Settings → Pages → Source: Deploy from a branch → Branch: `main` / `root` → Save.**

After a minute your app is live at `https://YOUR-USERNAME.github.io/mindly/`.
To update it later: edit the files, then `git add -A && git commit -m "update" && git push`.

---

## 3. Cloudflare Pages

1. Push the folder to GitHub first (steps above).
2. https://dash.cloudflare.com → **Workers & Pages → Create → Pages → Connect to Git.**
3. Pick the repo. Leave the build command **empty** and set the output directory to `/`.
4. Deploy. You get `https://mindly.pages.dev`, and you can attach your own domain free.

---

## 4. Just test it on your phone (no hosting)

With your phone and PC on the same Wi-Fi:

```bash
cd "D:/mind map"
python -m http.server 5599
```

Find your PC's local IP with `ipconfig` (look for IPv4, e.g. `192.168.1.7`), then open
`http://192.168.1.7:5599` on your phone. Stop the server with Ctrl+C.

Note: browsers only allow **Add to Home screen** over `https://` or `localhost`, so the
install prompt appears on a real host, not over this plain-http address.

---

## Installing it as a phone app

Once hosted over https, Mindly installs like a native app:

- **Android / Chrome** — open the site → ⋮ menu → **Add to Home screen** → **Install**
- **iPhone / Safari** — open the site → Share button → **Add to Home Screen**

It then opens fullscreen with no browser bars, using the icon in `icon.svg`.

## Where the data lives

Maps are stored in the browser's `localStorage`, on that device only. They are not
uploaded anywhere, so a map made on your laptop won't appear on your phone. To move
one across, use **File → Export JSON** on one device and **Import JSON** on the other.
Each host (a Netlify URL vs a GitHub Pages URL vs a local file) has its own separate
storage, so use one address consistently.
