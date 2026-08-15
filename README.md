# Charithra G — Portfolio

Interactive AI/ML engineering portfolio. Single self-contained `index.html`:
inline CSS + JS, Three.js via CDN, no build step and no dependencies.

**Live:** https://charithra754-boop.github.io/portfolio_indeed/

## What's in it

- **Neuron-field background (WebGL).** Biological neurons — soft somas with
  nuclei, curved dendrites, amber synaptic boutons — that progressively
  rectify into a digital neural network (square nodes, axis-aligned Manhattan
  traces) as you scroll. Action potentials travel the fibres throughout.
- **Per-project 3D visualisers.** Each case study drives its own scene:
  an anomaly-topology surface, a spike-embedding cloud, an orbital point
  cloud with a sweeping scan plane, and a 7-agent message mesh. All react to
  scroll position, hover and drag.
- **Iridescent hero orb.** Morphing icosahedron whose particle shell is tinted
  across a teal → violet → magenta → amber ramp that rotates over time.
- **Espresso dark theme.** Warm near-black base with copper/gold/bronze
  metallic accents; Plus Jakarta Sans paired with Cormorant Garamond italics.
- **Chibi mascot.** Inline SVG avatar in the nav, plus a seated version in the
  hero sipping an iced coffee that tips over when you reach Contact — the ice
  cubes then tumble across the hero under real 2D physics (gravity,
  restitution, rolling friction, angular momentum).

## Running locally

No tooling required — open the file, or serve it:

```bash
python3 -m http.server 8000
# http://localhost:8000
```

## Customising

The 3D scenes live in the `VIZ` object; each entry returns
`{ group, update(t, dt, ctx) }` and is bound to markup via `data-viz`.
Accent colour is inherited from the parent's `data-accent`, so changing
that attribute recolours both the card and its 3D scene.

Tuning knobs are marked with `// ---- CUSTOMIZE` comments:

| What | Where |
|---|---|
| Neuron count, spread, dendrites per cell | `initBackground` |
| Orb colour ramp | `SHELL_RAMP` in `VIZ.hero` |
| Embedding cloud density / filament reach | `VIZ.embedding` |
| Point-cloud resolution and shape | `VIZ.pointcloud` |
| Heatmap mesh resolution, wave function | `VIZ.heatmap` |
| Agent count and ring radius | `VIZ.agentgraph` |

## Performance

One shared `requestAnimationFrame` loop drives every scene. Off-screen
canvases skip rendering via `IntersectionObserver`, the loop halts entirely
when the tab is hidden, frame updates are capped (30fps on low-core or
reduced-motion devices), and render resolution is capped at 1.5× DPR.
Particle buffers are preallocated `Float32Array`s mutated in place, so the
JS heap stays flat (~10 MB) with no per-frame allocation.

Honours `prefers-reduced-motion`, and all content remains readable if WebGL
is unavailable.

## Accessibility

Semantic HTML5 landmarks, single-`h1` heading outline, skip link, visible
focus rings, labelled links, and `aria-hidden` on decorative canvases.
Metallic text on the espresso background measures 8:1–9.3:1 contrast
(WCAG AA requires 4.5:1).
