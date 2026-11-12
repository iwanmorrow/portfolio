# README.md

```markdown
# MORROW

A personal portfolio that happens to be a single HTML file.

Scroll down and a chrome shape morphs through four different geometries. Rings spin around it. Background objects drift in and out of focus. Scroll back up and it all reverses. That's the whole idea — the page is one continuous 3D scene, and scrolling is the only control.

I'm Morrow. I write mostly Rust, I'm interested in systems and security, and this site is a fairly direct translation of how I think about software: no unnecessary layers, no bundler, no framework pretending to be something it isn't.

---

## What's actually in here

The entire site is `index.html`. Open it, read it, edit it. Nothing is hidden behind a build step.

What's inside:

- **A Three.js scene** with a chrome object that morphs between four shapes as you scroll (organic → elongated → complex → compact). The morphing runs on the GPU via `morphAttributes`, not vertex-by-vertex JS.
- **Orbital rings** with small chrome particles moving along their paths. Different speeds, different planes.
- **Background geometry** — a torus, a sphere, a ring, an icosahedron — each rotating on its own axis at its own pace, with scroll parallax to give the whole thing depth.
- **Atmospheric particles**, ACES Filmic tone mapping, fog, vignette, film grain. It's dark on purpose.
- **Scroll choreography** with GSAP + ScrollTrigger. Every animation reverses when you scroll back up. Not just the scrub ones — the reveal animations too.
- **Lenis** for smooth scrolling, but it's wired into `gsap.ticker` as a single animation step. No duplicate RAF loops. That was a bug once. It's fixed.
- **A working scroll spy** — navbar and the right-side rail both track which section you're in.
- **Graceful degradation** — no WebGL? You get a static fallback glow. `prefers-reduced-motion`? Everything renders in its final state, no animation loops.

---

## Stack

```
HTML + CSS + vanilla JS
Three.js        (3D scene)
GSAP + ScrollTrigger  (scroll animation)
Lenis           (smooth scrolling)
Space Grotesk · Inter · JetBrains Mono
```

That's it. No React, no Vite, no Tailwind, no npm install.

---

## Running it

The site uses ES module imports, so opening `index.html` from your desktop won't work. You need a server.

```bash
python3 -m http.server 8080
```

Then `http://localhost:8080`.

Or, if you're deploying:

- **GitHub Pages** — push to a repo, `Settings → Pages → Deploy from branch → main`. Done.
- **Cloudflare Pages / Netlify / Vercel** — connect the repo, no build command, output directory `.`.

That's genuinely the whole setup.

---

## Editing it

Everything is in one file. Here's where to look:

**Personal details** — search for these strings:
- `hello@morrow.dev` — email
- `@iwanmorrow`, `@voobw`, `@morrow737` — socials
- `Donetsk region, Ukraine` — location line
- Images live in `img/` (`portrait.jpg`, `NL.png`, `SYSTEMA.png`, `EMV.png`)

**Palette** — CSS variables at the top:

```css
:root {
  --bg: #040406;
  --fg: #f4f4f4;
  --muted: #7a7a82;
  --line: #1a1a20;
  --silver: linear-gradient(135deg, #fff, #c8c8d0 40%, #888890 70%, #e8e8ec);
}
```

Change `--bg` and `--fg` and the whole site shifts. The chrome materials use `MeshStandardMaterial` with `metalness: 1` — they reflect the environment, so you don't need to touch them unless you want a different finish.

**Stack section** — plain HTML. Each `.stack-item` has a `--pct` on the inline style. Bar fills automatically.

**Projects** — each is an `<article class="project-chapter">`. Copy one to add a project. Delete one to remove it. The `.project-status` pill says `Active`, `In development`, `Prototype`, `Concept`, or `Archived` — pick the one that's actually true.

**The 3D shapes** — four functions in the module script:

```js
function shapeOrganic(x, y, z) { ... }
function shapeElongated(x, y, z) { ... }
function shapeComplex(x, y, z) { ... }
function shapeCompact(x, y, z) { ... }
```

Each takes a unit sphere vertex and returns a new position. Change any of them and the morphing updates automatically. The interpolation happens in the shader.

---

## Accessibility

Not an afterthought — the site respects `prefers-reduced-motion` (Lenis doesn't load, GSAP timelines don't create, the 3D scene renders one static frame), keyboard navigation works, the mobile menu announces its state, and active nav links get `aria-current`. If WebGL is missing, the canvas hides and a CSS glow takes its place. Content stays fully usable either way.

---

## Performance

- One WebGL context for the whole site, not one per section
- `InstancedMesh` for orbital particles — 36 spheres in a single draw call
- DPR capped at 2 (1.5 on wide screens)
- Render loop gated by `IntersectionObserver` — stops when the canvas is off-screen
- On mobile: fewer particles, sparser sphere geometry (90×45 instead of 140×70)
- No animated blur filters, no shadows on moving elements

It runs at 60fps on a mid-range laptop and holds together on phones. On a very old device it drops to a static frame rather than stuttering.

---

## Browser support

Chrome, Edge, Firefox (last 2 versions), Safari 16+, mobile Safari 16+, Chrome Android.

Needs `importmap` support — that's all modern browsers as of 2023.

---

## Credits

- [Three.js](https://threejs.org/) — the 3D engine
- [GSAP](https://gsap.com/) + ScrollTrigger — scroll choreography
- [Lenis](https://github.com/darkroomengineering/lenis) — smooth scrolling
- Space Grotesk, Inter, JetBrains Mono — via Google Fonts

---

## License

Content, copy, and design are mine. Third-party libraries keep their own licenses (MIT for Three.js and Lenis, GSAP's standard license).

If you're reading this because you want to build something similar — take the ideas, not the code. Your portfolio should look like you, not like mine.

---

## Contact

- **Email** — hello@morrow.dev
- **GitHub** — [@iwanmorrow](https://github.com/iwanmorrow)
- **Telegram** — [@voobw](https://t.me/voobw)
- **TikTok** — [@morrow737](https://tiktok.com/@morrow737)

---

*Building systems that matter.*
```
