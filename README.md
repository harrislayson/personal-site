# personal-site

Harris Layson's personal website: a desk with a computer on it. Press Start, and the
screen boots into a small desktop OS with a menu bar, folders, a dock, and draggable
windows covering education, work, projects, photos, books, and a résumé.

Live at **https://harrislayson.github.io/personal-site/** (once GitHub Pages is enabled).

## Structure

```
index.html    the entire site: markup, CSS, and JavaScript in one file
photos/       optimised JPEGs (1100px long edge) plus one book cover
```

There is no build step and no dependencies. Open `index.html` in a browser and it runs.

## How it fits together

The page is a single self-contained file. The room, the Macintosh casing, the posters,
and the plant are all CSS. Inside the screen is a small window manager:

- Any element with `data-open="<window-id>"` opens the matching `.window` element.
  The dock, the desktop folders, and several in-page links all use this.
- Windows can be focused, minimised, maximised, and dragged by their title bar.
- The résumé is stored in the page as a base64 PDF (`#cv-data`) and turned into a blob
  URL at runtime, so the inline viewer and the download link both work offline.

To add a window, drop in a `.window` section with an `id`, a `.titlebar`
(close / minimise / maximise buttons plus a `.window-title`), and a `.content` div.
No JavaScript changes are needed.

## Styling

The CSS is minified and built up as a series of override blocks, each one layered on the
last. The final block before `</style>` is the current design layer, modelled on a modern
macOS desktop. **Put new screen styles there** so they win the cascade.

## Photos

Everything in `photos/` is optimised with:

```
sips -Z 1100 -s format jpeg -s formatOptions 55 input.jpg --out photos/output.jpg
```

Book covers are served from the [Open Library Covers API](https://openlibrary.org/dev/docs/api/covers)
rather than stored here, apart from one title Open Library does not carry.

## Small screens

Below 820px wide (or on a touch device under 520px tall) the site hides itself and shows
a notice pointing visitors to a desktop, since the window manager needs the room.

## Local preview

```bash
python3 -m http.server 4177
```

Then open http://localhost:4177/. Serving over HTTP rather than opening the file
directly keeps the relative `photos/` paths working the same way they will in production.
