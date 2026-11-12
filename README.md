# MORROW

A personal portfolio built around one idea: making a website feel less like a website.

MORROW is a small experiment in 3D graphics, motion and web development. The entire page is built around a single Three.js scene that changes as you scroll.

A chrome object moves through different shapes, surrounded by rotating rings and floating geometry. Scroll down and the scene evolves. Scroll back up and everything returns.

No separate scenes for each section. Just one continuous experience.

## About

I'm Morrow, an independent developer interested in systems programming, security and the software behind the things we use every day.

I mostly work with Rust and enjoy building things that are simple in structure but interesting under the hood.

This portfolio is one of those experiments.

## Built with

- HTML, CSS and vanilla JavaScript
- Three.js for the 3D scene
- GSAP and ScrollTrigger for animation
- Lenis for smooth scrolling

Everything lives in a single `index.html` file. There is no build process or complicated setup.

## A few things worth mentioning

- GPU-based geometry morphing between four shapes
- Procedurally arranged orbital rings and particles
- Scroll-driven animations that work in both directions
- Responsive layouts and mobile-specific optimizations
- Reduced-motion support and a fallback for devices without WebGL

## Running locally

You'll need a local HTTP server because the project uses ES modules.

```bash
python3 -m http.server 8080
```

Open `http://localhost:8080` in your browser.

## Structure

```text
MORROW/
├── index.html
├── img/
│   ├── portrait.jpg
│   ├── NL.png
│   ├── SYSTEMA.png
│   └── EMV.png
└── README.md
```

## Credits

- [Three.js](https://threejs.org/)
- [GSAP](https://gsap.com/)
- [Lenis](https://github.com/darkroomengineering/lenis)
- Space Grotesk, Inter and JetBrains Mono

## Contact

- Email: hello@morrow.dev
- GitHub: [@iwanmorrow](https://github.com/iwanmorrow)
- Telegram: [@voobw](https://t.me/voobw)
- TikTok: [@morrow737](https://tiktok.com/@morrow737)

---

*Building systems that matter.*
