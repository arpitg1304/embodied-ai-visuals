# Animation Development Guidelines

Lessons learned from building animations for this project. Follow these to avoid common pitfalls.

## File Structure

Each animation is a **standalone HTML page** (`<!DOCTYPE html>`, `<html>`, `<head>`, `<body>`). It runs inside an `<iframe>` on the landing page, giving it a clean JS execution context.

```
animations/
  your_animation.html    ← standalone HTML page
```

### Body styling

- Use `padding: 24px 32px; margin: 0` — **never** `max-width: 720px` or `margin: 0 auto`. The iframe gives it full width; don't constrain it.
- Background: `#0d1117` (dark theme preferred). If using light theme, add `prefers-color-scheme:dark` media queries.

## Step-based Animations (the most common pattern)

Most animations walk through 3–6 steps with SVG visuals. Here's the reliable pattern:

### Use full SVG swap with opacity transition

```css
.canvas-wrap svg {
  opacity: 0;
  transition: opacity 0.4s ease;
}
.canvas-wrap svg.visible {
  opacity: 1;
}
```

```js
function goTo(idx) {
  const svg = document.getElementById('viz');
  svg.classList.remove('visible');       // fade out
  setTimeout(() => {
    renderStep(idx);                     // swap content
    svg.classList.add('visible');         // fade in
  }, 200);
}
```

**Why:** Setting `innerHTML` replaces the entire SVG DOM. A single fade transition on the whole SVG is smooth and predictable. No elements flash or disappear.

### DO NOT use staggered CSS fade-ins

```css
/* BAD — elements flash visible before delay kicks in */
.fade-in { animation: fadeIn 0.5s ease forwards; }
<g class="fade-in" style="animation-delay: 0.5s">  <!-- flashes -->
```

Even with `opacity: 0` as the initial state, this approach causes timing issues:
- Elements with `animation-delay` can flash before going invisible
- SVG `<animate>` elements with `begin` delays run independently of CSS
- When auto-play advances, everything restarts and animations fire out of sync

### Use SVG `<animate>` for continuous motion only

Good uses of `<animate>`:
- Pulsing opacity: `values="0.5;0.9;0.5"` with `repeatCount="indefinite"`
- Flowing dashed lines: `stroke-dashoffset` animated in a loop
- Scanning/sweep effects that repeat

Bad uses:
- One-shot animations with `fill="freeze"` — these fire once and die, look broken on step re-entry
- Anything with `begin` delays that needs to sync with CSS transitions

## Auto-play

Add a play/pause button. Auto-start after 2–3 seconds on page load. Use 5 seconds per step (4s is too fast for reading).

```js
let autoTimer = null;
let playing = false;

function togglePlay() {
  if (playing) { stopPlay(); return; }
  playing = true;
  advanceAuto();
}

function advanceAuto() {
  if (!playing) return;
  goTo((current + 1) % STEPS.length);
  autoTimer = setTimeout(advanceAuto, 5000);
}

function stopPlay() {
  playing = false;
  clearTimeout(autoTimer);
}
```

Stop auto-play when the user manually navigates (clicks dot, arrow, or presses key).

## Navigation

Always support:
- Dot indicators (clickable)
- Prev/Next buttons
- Arrow keys (Left/Right)
- Progress bar showing step N of M

## SVG Tips

- Use `viewBox="0 0 700 360"` — gives enough room for layouts. Adjust height if needed.
- Keep text sizes between 7–14px. Smaller is unreadable; larger overwhelms.
- Use the project color palette:
  - `#58a6ff` — accent blue (links, highlights)
  - `#1D9E75` — green (positive, success, selected)
  - `#D85A30` — orange (warning, secondary option)
  - `#A371F7` — purple (processing, encoder, model)
  - `#484f58` / `#30363d` — borders, muted elements
  - `#8b949e` / `#6e7681` — secondary and tertiary text
  - `#161b22` — card/panel fill
  - `#1c2333` — subtle surface

## Registration

After building the animation:

1. Add to `ANIMATIONS` array in `index.html`:
```js
{
  id: 'your_animation',        // filename without .html
  title: 'Your Title',
  description: 'One-liner.',
  tag: 'World Models',         // filter tag
  category: 'Learning',        // broad category
  paper: 'https://arxiv.org/abs/...',  // optional
},
```

2. Add to the animations table in `README.md`
3. Optionally add an SVG preview to the `PREVIEWS` object in `index.html`

## Testing

```bash
python3 -m http.server 8000
```

Check:
- Animation loads in iframe (no blank screen)
- All steps render without overlapping text
- Auto-play cycles smoothly
- Manual navigation (dots, arrows, keys) works
- No console errors
- Looks reasonable on a narrow viewport (~375px wide)
