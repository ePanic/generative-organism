# 🧬 Generative Organism

> An aquarium of mathematical life — interactive generative art powered by p5.js and attractor mathematics

<div align="center">

![Generative Organism](https://img.shields.io/badge/p5.js-1.9.0-FF6B6B?style=for-the-badge&logo=javascript)
![WebGL](https://img.shields.io/badge/WebGL-3D-4488FF?style=for-the-badge)
![Netlify](https://img.shields.io/badge/Netlify-Live-00C7B7?style=for-the-badge&logo=netlify)

**[🌐 Live Demo](https://generative-organism.netlify.app)**

</div>

---

## ✨ Features

### 🎨 8 Unique Creature Types
- **ORGANISM** — orbital parametric attractor
- **MEDUSA-X** — fluid jellyfish-like petal motion
- **CTENOPHORA** — elongated ribbon dancers
- **SIPHON** — spiral chain formations
- **RADIOLARIA** — radial spines with symmetry
- **BIOLUME** — diffuse glowing clouds
- **NAUTILOID** — tight mathematical spirals
- **XENOCORAL** — branching coral structures

### 🔢 4 Mathematical Visualizations
- **MANDELBROT** — progressive fractal rendering with interactive zoom
- **JULIA** — complex plane iteration with real-time parameters
- **LISSAJOUS** — 3D harmonic knots
- **CLIFFORD** — strange attractor point clouds

### 🎮 Interactive Controls
- **TYPE buttons** — switch creature type instantly
- **3D toggle** — flat view or slow auto-rotating 3D with true depth
- **Universal sliders** — control all creatures with:
  - DENSITY, SPEED, SIZE, OPACITY, GLOW, WEIGHT, TRAIL
  - COLOR SPEED, SPIN, HUE, SYMMETRY
  - Advanced: K_AMP, FREQUENCIES, TWIST, WAVE, DEPTH, SQUEEZE
- **COLOR palette** — 13 hand-crafted color schemes (Vibrant, Synthwave, Inferno, Aurora, Biolume, etc.)
- **Double-click MANDELBROT** — zoom into any point

### 🎯 Responsive Design
- **Desktop** — full controls in collapsible bottom panel
- **Mobile** — pinch-to-zoom, simplified touch interface
- **Smooth rendering** — P2D buffer with trail fade effect

### 🚀 WebGL 3D with Perspective
- 3D auto-rotate with X, Y, Z axis rotation
- Perspective depth scaling for true spatial effect
- Smooth camera inertia physics

---

## 🎯 How to Use

1. **Select a creature** — click TYPE buttons to switch (replaces current)
2. **Open controls** — tap the creature to reveal parameter sliders
3. **Tweak appearance** — adjust DENSITY, SPEED, SIZE, GLOW, TRAIL, etc.
4. **Change palette** — click COLOR dots in top bar for instant recolor
5. **Enable 3D** — hit "3D OFF" button for slow auto-rotating view
6. **Zoom** — scroll wheel (desktop) or pinch (mobile) to zoom
7. **Reset** — RESET button clears and spawns fresh ORGANISM

### Special Interactions
- **MANDELBROT/JULIA** — double-click to zoom into that pixel (40% zoom)
- **Fractal sliders** — real-time parameter control with progressive render
- **Trail effect** — lower TRAIL value for ghosting, higher for solid

---

## 🛠 Tech Stack

- **p5.js** — creative coding framework
- **WebGL** — 3D rendering (`p.WEBGL`)
- **P2D Graphics Buffer** — offscreen rendering with alpha trails
- **Attractor Mathematics** — parametric equations driving each creature
- **Netlify** — deployment & hosting

---

## 📊 Architecture

```
index.html (single file, ~975 lines)
├── Palettes (13 HSB-based color schemes)
├── Entity class
│   ├── drawAttractor() — unified parametric math for 8 creature types
│   ├── drawFractalProgressive() — Mandelbrot/Julia with smooth coloring
│   ├── drawLissajous() — 3D harmonic knots
│   └── drawClifford() — strange attractor
├── p5 sketch (WebGL canvas + P2D buffer)
│   ├── setup() — canvas + graphics buffer initialization
│   ├── draw() — camera physics + entity rendering
│   ├── mouse/touch controls — hit testing + zoom
│   └── doubleClicked() — fractal zoom-into-point
└── UI (topbar + control panel)
    ├── Type selector (creature buttons)
    ├── Palette dots (instant recolor)
    ├── Math selector (fractal buttons)
    ├── Per-entity sliders
    └── 3D toggle + info modal
```

---

## 🎨 Key Parameters

All creatures share **universal sliders**:

| Slider | Range | Effect |
|--------|-------|--------|
| DENSITY | 500–8000 | point count per frame |
| SPEED | 0–0.2 | animation speed |
| SIZE | 0.1–3 | scale multiplier |
| OPACITY | 10–255 | point brightness |
| GLOW | 0–8 | halo effect intensity |
| WEIGHT | 0.5–4 | stroke thickness |
| TRAIL | 2–120 | fade persistence (higher = ghosting) |
| SYMMETRY | 1–8 | rotational copies |
| HUE | 0–360 | color shift |

**Creature-specific parameters** (K_AMP, FREQUENCIES, SQUEEZE, etc.) fine-tune the mathematical formula for each type.

---

## 🧬 How Creatures Work

Each creature (except fractals) uses a **unified attractor formula**:

```javascript
const k = k_amp * cos(x / x_freq) * cos(y / y_freq)
const e = y / e_scale - e_offset
const d = (k² + e²) / d_denom + d_offset
const c = d/2 + e/99 - t/t_div

const x = (q + wave) * sin(c)
const y = (q + d*d_y) * cos(c) * squeeze
```

Different default parameters for each type create distinct visual personalities — same math, different souls.

---

## 🚀 Deployment

**Live:** https://generative-organism.netlify.app

Deploy locally:
```bash
npx netlify deploy --dir . --prod
```

---

## 🎬 Adding Custom Creatures

To create a new creature type:

1. Add to `TYPE_DEFS` object with unique defaults:
```javascript
'MY_CREATURE': {
  defaults: { ...C, k_amp: 12, x_freq: 8, /* ... */ },
  sliders: [...COMMON_SLIDERS, ...ATTRACTOR_SLIDERS]
}
```

2. Add HTML button:
```html
<button class="btn btn-spawn" data-type="MY_CREATURE">MY_CREATURE</button>
```

3. Optionally add custom `draw()` method in Entity class.

---

## 🎨 Color Palettes

13 HSB-based palettes with dynamic animation:
- **Vibrant**, **Synthwave**, **Inferno**, **Acid**, **Neon City**
- **Aurora**, **Deep Space**, **Lava**, **Ice**, **Mono**
- **Biolume**, **Abyssal**, **Coral Sea**

Each palette responds to the **COLOR_SPEED** slider for animated hue cycling.

---

## 📱 Browser Support

- Chrome/Edge (WebGL, touch optimal)
- Firefox (WebGL)
- Safari (WebGL, pinch-zoom works great)
- Mobile browsers (responsive touch controls)

---

## 🙏 Inspiration

Inspired by the mathematical beauty of:
- [Josephine Miller](https://www.instagram.com/josephinemiller/) — generative art pioneer
- Strange attractors & chaos theory
- Organic morphology in nature

---

## 📝 License

MIT — feel free to fork, modify, and create your own creatures.

---

## 🔮 Future Ideas

- [ ] Save/load custom creature presets
- [ ] Animation export (GIF/MP4)
- [ ] Sound reactive mode
- [ ] Multi-creature harmony (interact with each other)
- [ ] GPU particle system for 10K+ points
- [ ] Community creature gallery

---

<div align="center">

**Made with 🧬 + 💙 using p5.js**

[Live Demo](https://generative-organism.netlify.app) — [GitHub](https://github.com/ivicapanic/generative-organism)

</div>
