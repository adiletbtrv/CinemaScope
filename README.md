# CinemaScope

A premium, zero-dependency film discovery platform built with vanilla HTML, CSS, and JavaScript. Powered by the TMDB API.

![](https://github.com/user-attachments/assets/fdd09c86-0760-47e8-8499-26833095b83e)
![](https://github.com/user-attachments/assets/c8f6dad7-94e9-461c-9167-3ac34911b368)

<table>
  <tr>
    <td><img src="https://github.com/user-attachments/assets/c14b6a9e-e578-4e75-9bcf-9b58b8a549c2" /></td>
    <td><img src="https://github.com/user-attachments/assets/f277f493-49f3-46ee-a386-641c678c72f0" /></td>
  </tr>
  <tr>
    <td><img src="https://github.com/user-attachments/assets/e6b04b79-2306-4e14-bd9e-67b84f2b097a" /></td>
    <td><img src="https://github.com/user-attachments/assets/a72589d8-f41f-4945-8260-08c6d8abdd1f" /></td>
  </tr>
</table>

---

## Tech Stack

| Layer | Choice | Reason |
|---|---|---|
| Markup | HTML5 (semantic) | `<aside>`, `<nav>`, `<main>`, `<header>`, `role` attributes throughout |
| Styles | CSS3 | Custom properties, `backdrop-filter`, `clamp()`, CSS Grid, no preprocessor |
| Logic | Vanilla JS (ES2022) | `'use strict'`, modular object pattern, `async/await`, zero dependencies |
| Data | TMDB API v3 | Film metadata, backdrops, trailers, ratings |
| Persistence | `localStorage` | Saved library survives page refresh |
| Fonts | Instrument Serif + Geist | Display/UI type pairing via Google Fonts |
| Icons | Font Awesome 6.5 | Thin icon set via CDN |

---

## Project Structure

```
cinemascope/
├── index.html      # Semantic HTML shell — layout, overlays, SVG logo
├── styles.css      # Design system — tokens, components, responsive breakpoints
└── script.js       # Application logic — State, Store, API, Loader, Sheet, Search
```

### JavaScript Architecture

The script is organised into single-responsibility modules:

```
CONFIG          Global constants (API key, base URL, storage key)
SECTIONS        Section config map — hero function + rows function per section
State           Runtime state (current section, hero movie, cached trailer URL)
Store           localStorage abstraction — CRUD for the saved library
API             TMDB fetch wrapper — get(), trending(), details(), trailer(), search()
UI              DOM sync helpers — badge counts, active tabs, hero save button
Hero            Hero section renderer — backdrop, title, attrs, score, trailer
Loader          Section orchestrator — wires hero + shelf rendering per section
buildCard()     Card factory — renders article element with all event listeners
buildShelf()    Shelf factory — header + grid + stagger animation
Handlers        Cross-cutting actions (toggleSave with icon + toast sync)
Sheet           Detail and account sheet open/close
Search          Command palette open/close/query/render
Toast           Ephemeral notification with auto-dismiss
```

---

## Getting Started

No build step, no package manager, no configuration.

```bash
git clone https://github.com/adiletbtrv/cinemascope.git
cd cinemascope
open index.html
```

Or serve it locally for proper API CORS behaviour:

```bash
# Python
python -m http.server 8080

# Node
npx serve .
```

Then open `http://localhost:8080`.

---

## API Key

The project ships with a public TMDB API key for demonstration. To use your own:

1. Create a free account at [themoviedb.org](https://www.themoviedb.org/)
2. Go to **Settings → API** and generate a key
3. Replace the value in `script.js`:

```js
const CONFIG = {
  apiKey: 'your_api_key_here',
  ...
};
```

---

## Responsive Behaviour

| Breakpoint | Layout |
|---|---|
| `> 1100px` | Full sidebar with labels, wide shelf grid |
| `740px – 1100px` | Icon-only sidebar (collapsed), medium grid |
| `< 740px` | Sidebar hidden, glass topbar + bottom dock |
| `< 420px` | Compact grid, smaller hero title |

Overlays (command palette, sheets) adapt to bottom-sheet pattern on mobile with rounded top corners and safe-area padding for notched devices.

---

## Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| `⌘K` / `Ctrl+K` | Open command palette |
| `Esc` | Close active overlay (palette → sheets, priority order) |

---

## Design Decisions

**No framework.** The component count is small enough that vanilla JS with a clear module pattern is faster to load, easier to audit, and has zero dependency surface.

**CSS custom properties as a design system.** Every colour, radius, easing curve, and layout dimension lives in `:root`. Changing the entire visual theme is a single block edit.

**`backdrop-filter` for depth.** Glass-morphism effects on the topbar, dock, overlays, and card actions create layered depth without heavyweight shadow stacks.

**`Instrument Serif` for display type.** Editorial serif for titles and stats gives the UI a cinematic character that pure sans-serif stacks can't achieve. `Geist` handles all interface text cleanly at small sizes.

**Staggered entrance animations in pure CSS timing.** Card grids animate in with `transition-delay` increments calculated per-index in JS, with no animation library required.

---

## Browser Support

All modern browsers. Requires:
- `backdrop-filter` (Chrome 76+, Safari 9+, Firefox 103+)
- `CSS Grid` and `clamp()` (universally supported)
- `async/await` and `localStorage` (universally supported)

---

## License

MIT — see [LICENSE](LICENSE) for details.

---

## Author

Built by **Adilet Batyrov**

- GitHub: [github.com/adiletbtrv](https://github.com/adiletbtrv)
- LinkedIn: [linkedin.com/in/adilet-batyrov](https://www.linkedin.com/in/adilet-batyrov/)
