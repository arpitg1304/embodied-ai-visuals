# Embodied AI Visuals

Interactive animations explaining core concepts in robotics and embodied intelligence.

**Live site:** [arpitg1304.github.io/embodied-ai-visuals](https://arpitg1304.github.io/embodied-ai-visuals/)

## Animations

| Animation | Description |
|-----------|-------------|
| VLA Model Explainer | Step-by-step walkthrough of Vision-Language-Action models — from camera input to robot action output |

## Adding a new animation

1. Drop a self-contained `.html` file into `animations/`
2. Add an entry to the `ANIMATIONS` array in `index.html`:
   ```js
   { id: 'filename_without_extension', title: '...', description: '...', tag: '...' }
   ```
3. Push — the site updates automatically via GitHub Pages.

## Local development

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000`.
