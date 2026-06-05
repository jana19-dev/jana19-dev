# Project screenshots

Drop screenshots here and they show up on the site automatically — no build step, no code edit needed.

## How it works

Each project on the site has a **slug** (defined in the `PROJECTS` array near the bottom of [`/index.html`](../../index.html)). Screenshots for a project live in a folder named after that slug:

```
assets/projects/<slug>/
  1.png    ← cover (shown on the card)
  2.png
  3.png
  …
```

When the page loads it looks for `1`, then `2`, then `3`… and stops at the first missing number. The first image becomes the card's cover thumbnail; clicking it opens a full-screen lightbox gallery of all of them.

## Naming rules

- **Number from `1`, with no gaps** — `1`, `2`, `3`, … Image `1` is the cover.
- **One format per folder.** Supported: `.png`, `.jpg`, `.jpeg`, `.webp`. PNG is recommended for UI screenshots. Use the same extension for every image in a given folder.
- The folder name **must exactly match the project's `slug`** in `index.html`.

### Example

```
assets/projects/pennywise/1.png
assets/projects/pennywise/2.png
assets/projects/pennywise/3.png
```

→ Pennywise's card shows `1.png` as its cover and opens a 3-image gallery.

## Image guidance

- Export around **1600px wide**; landscape (≈16:10) looks best as a cover, but any size works (covers are cropped to fit, the lightbox shows the full image).
- **Compress** them — aim for **< ~300 KB each** (WebP or an optimized PNG). Large images slow the page down.
- Screenshots load lazily, so extra images only download when needed.

## Adding a brand-new project

1. Open [`/index.html`](../../index.html) and find the `PROJECTS` array (near the bottom).
2. Copy one entry, give it a unique `slug`, and fill in `name`, `year`, `description`, `tags`, and either `live`/`github` links **or** `private: true` (shows a subtle "Client work" badge — perfect for client work you can't link publicly but can show with screenshots).
3. Create a folder here named exactly `<slug>` and drop in `1.png`, `2.png`, …

That's it. Templates are already in the array (the `draft: true` ones) — copy one and remove the `draft` flag to publish it.

## Per-project options (in the `PROJECTS` array)

| Field          | Effect                                                                 |
| -------------- | --------------------------------------------------------------------- |
| `private: true`| Shows a "Client work" badge instead of Live/GitHub links.            |
| `draft: true`  | Hides the project from the page (used for the copy-paste templates).  |
| `shots: N`     | Use exactly `N` screenshots — skips auto-detection and keeps the browser's network tab clean. |
| `shots: 0`     | Disable screenshots for this project entirely.                        |
| _(omit `shots`)_ | Fully automatic — detects however many images you drop in.          |

## A note on the network tab

Auto-detection works by requesting images until one is missing, so a project **without** screenshots yet (or the image right after your last one) produces a harmless background `404`. It does not affect anything users see. To silence it for a finished project, set `shots: N` to its exact screenshot count, or `shots: 0` for projects you won't add screenshots to.
