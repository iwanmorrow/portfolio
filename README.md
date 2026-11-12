# README.md

```markdown
# MORROW

A cinematic, scroll-driven personal portfolio for **Morrow** — independent developer focused on systems software and cybersecurity.

Single-file HTML. No build step. No frameworks.

---

## About

MORROW is not a template portfolio. It's a personal site built around three ideas:

- **Honest positioning** — the site describes real work with real statuses, not inflated titles or percentages.
- **Cinematic pacing** — sections are treated as scenes; scrolling drives a continuous 3D narrative.
- **Restraint** — a monochrome visual language with chrome materials, chrome rings and chrome geometry instead of neon.

The site is intentionally a single `index.html`. It loads only what it needs, works without a bundler, and degrades gracefully when WebGL is unavailable.

---

## Features

- **Live Three.js scene** with a chrome morphing centerpiece that transitions between four geometric states as you scroll.
- **Orbital system** — thin orbit lines with chrome particles traveling along their paths.
- **Background geometry** — depth-layered chrome objects with continuous rotation and scroll parallax.
- **Ambient particles**, ACES Filmic tone mapping, exponential fog, vignette and film grain.
- **Scroll-driven morphing** via `morphAttributes` (GPU-side), synced to `ScrollTrigger`.
- **Bidirectional animations** — everything plays forward and reverses cleanly on scroll-up.
- **Lenis smooth scrolling**, wired into `gsap.ticker` as a single animation step.
- **Scroll spy navigation** — navbar and right-side progress rail track the active scene.
- **Accessibility** — respects `prefers-reduced-motion`, keyboard-navigable, `aria-current` on active links.
- **Responsive** — mobile menu, tuned geometry and reduced particle counts on touch devices.

---

## Stack

| Layer | Technology |
|---|---|
| Markup & Styling | Semantic HTML5 + Vanilla CSS |
| Typography | Space Grotesk · Inter · JetBrains Mono |
| 3D | Three.js r160 (ESM via importmap) |
| Scroll & Animation | GSAP + ScrollTrigger |
| Smooth Scroll | Lenis |
| Interaction | Vanilla JS |

**No frameworks, no bundlers, no build step.**

---

## Project Structure

```
morrow/
├── index.html
└── img/
    ├── portrait.jpg
    ├── NL.png
    ├── SYSTEMA.png
    └── EMV.png
```

---

## Getting Started

The site uses ES module imports, so it must be served over HTTP — opening the file directly via `file://` will not work in most browsers.

**Any static server works:**

```bash
# Python
python3 -m http.server 8080

# Node
npx serve .
```

Then open `http://localhost:8080`.

**Deployment** — drop the folder into any static host:

- **GitHub Pages** — push, then enable Pages from `Settings → Pages → Deploy from branch → main`.
- **Cloudflare Pages / Netlify / Vercel** — connect the repo, no build command, output directory `.`.

---

## Customization

Everything lives in `index.html`. Common edits:

**Personal details** — search and replace:

- `hello@morrow.dev` — contact email.
- `@iwanmorrow`, `@voobw`, `@morrow737` — social handles.
- `Donetsk region, Ukraine` — location line.
- Portrait and project images in the `img/` folder.

**Colors & typography** — CSS custom properties at the top of `<style>`:

```css
:root {
  --bg: #040406;
  --fg: #f4f4f4;
  --muted: #7a7a82;
  --line: #1a1a20;
  --silver: linear-gradient(135deg, #fff 0%, #c8c8d0 40%, #888890 70%, #e8e8ec 100%);
  --mono: 'JetBrains Mono', monospace;
  --sans: 'Inter', sans-serif;
  --display: 'Space Grotesk', sans-serif;
}
```

Changing `--bg`, `--fg`, `--muted`, `--line` and `--silver` shifts the entire palette.

**Stack section** — plain HTML. Each `.stack-item` accepts a `--pct` custom property that controls the bar fill width.

**Projects** — each `<article class="project-chapter">` is independent. The `.project-status` pill shows `Active`, `In development`, `Prototype`, `Concept`, or `Archived`.

**3D shapes** — four functions inside the module script:

```js
function shapeOrganic(x, y, z) { ... }
function shapeElongated(x, y, z) { ... }
function shapeComplex(x, y, z) { ... }
function shapeCompact(x, y, z) { ... }
```

Each takes a unit-sphere vertex and returns a new `[x, y, z]`. Three.js handles the interpolation between them via `morphAttributes`.

---

## Accessibility

- Keyboard-focusable interactive elements.
- Mobile menu announces state via `aria-expanded`.
- Active nav links receive `aria-current="page"`.
- `prefers-reduced-motion` disables Lenis, GSAP timelines and reveal animations; the 3D scene renders one static frame.
- WebGL absence hides the canvas and shows a CSS fallback glow — content remains fully usable.
- Touch devices skip mouse parallax and magnetic hover.

---

## Performance

- **Single WebGL context** for the whole site.
- **Instanced meshes** for orbital particles (one draw call).
- **DPR cap** at 2 (1.5 on wide screens).
- **Render loop gated** by `IntersectionObserver`.
- **Reduced geometry and particles on mobile**.
- **No CSS blur filters or animated box-shadows**.

---

## Browser Support

Chrome / Edge / Firefox (last 2 versions), Safari 16+, mobile Safari 16+, Chrome Android.

Requires `importmap` support (all modern browsers, 2023+).

---

## Credits

- **Design & Development** — Morrow
- **3D Engine** — [Three.js](https://threejs.org/)
- **Scroll Animation** — [GSAP](https://gsap.com/) · ScrollTrigger
- **Smooth Scrolling** — [Lenis](https://github.com/darkroomengineering/lenis)
- **Fonts** — Space Grotesk · Inter · JetBrains Mono via Google Fonts

---

## License

Personal portfolio. Content, copy and design are © Morrow. Third-party libraries retain their own licenses (MIT for Three.js, GSAP Standard License, Lenis MIT).

If you want to build something similar — take the ideas, not the code. A portfolio should look like you, not like someone else's website.

---

## Contact

- **Email** — hello@morrow.dev
- **GitHub** — [@iwanmorrow](https://github.com/iwanmorrow)
- **Telegram** — [@voobw](https://t.me/voobw)
- **TikTok** — [@morrow737](https://tiktok.com/@morrow737)

---

<p align="center"><sub>Building systems that matter.</sub></p>
```
