# Contributing to Embodied AI Visuals

Thanks for your interest in contributing! This project aims to build a collection of interactive animations that make robotics and embodied AI concepts accessible to everyone.

## Adding a new animation

### 1. Create the animation file

Copy the template:

```bash
cp animations/_template.html animations/your_animation_name.html
```

### 2. Build your animation

Your file is an HTML fragment (no `<html>` or `<body>` tags) that gets injected into the main page. Keep it self-contained with inline `<style>` and `<script>` blocks.

**Use the parent page's CSS variables** for consistent theming:

| Variable | Usage |
|----------|-------|
| `--color-bg` | Page background |
| `--color-surface` | Card/panel background |
| `--color-border` | Primary borders |
| `--color-text-primary` | Main text |
| `--color-text-secondary` | Secondary text |
| `--color-text-tertiary` | Subtle/muted text |
| `--color-accent` | Accent blue |
| `--color-accent-subtle` | Accent with low opacity |
| `--color-background-secondary` | Secondary backgrounds |

**Tips:**
- SVG-based visuals scale well and look great
- Keep animations smooth (use `requestAnimationFrame` for canvas, CSS `@keyframes` for simple effects)
- Test on mobile viewports too
- Prefix CSS class names to avoid collisions (e.g., `.vla-container` not `.container`)

### 3. Register the animation

Add an entry to the `ANIMATIONS` array in `index.html`:

```js
{
  id: 'your_animation_name',        // filename without .html
  title: 'Your Animation Title',
  description: 'What this animation teaches.',
  tag: 'VLA',                        // short category tag
  category: 'Perception',            // section grouping
},
```

**Categories:** Perception, Planning, Control, Learning (or propose a new one).

### 4. (Optional) Add a card preview

Add a mini SVG to the `PREVIEWS` object in `index.html` to show on the card before someone clicks it.

### 5. Test locally

```bash
python3 -m http.server 8000
# Open http://localhost:8000
```

### 6. Submit a pull request

- Keep your PR focused on one animation
- Include a screenshot or GIF in the PR description
- Make sure the animation loads and runs without errors

## Other contributions

- **Bug fixes** and **accessibility improvements** are always welcome
- **Design improvements** to the landing page — open an issue first to discuss
- **Documentation** — help improve this guide or the README

## Code style

- No build tools or dependencies — everything is vanilla HTML/CSS/JS
- Keep files self-contained
- Use semantic, readable variable names in your animation code
