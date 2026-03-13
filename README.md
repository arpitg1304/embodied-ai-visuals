# Embodied AI Visuals

Interactive animations explaining core concepts in robotics and embodied intelligence.

**Live site:** [arpitg1304.github.io/embodied-ai-visuals](https://arpitg1304.github.io/embodied-ai-visuals/)

## Animations

| Animation | Category | Description |
|-----------|----------|-------------|
| VLA Model Explainer | Perception | Step-by-step walkthrough of Vision-Language-Action models — from camera input to robot action output |
| Sim-to-Real Gap Explainer | Learning | Why sim-trained policies fail in the real world and how domain randomization bridges the gap |

## Features

- **No dependencies** — pure HTML/CSS/JS, zero build step
- **Dark themed** — easy on the eyes
- **Embeddable** — copy iframe embed code for any animation to use in your blog or slides
- **Mobile friendly** — responsive layout that works on any device
- **Auto-deploy** — push to `main` and GitHub Actions deploys to Pages

## Adding a new animation

1. Copy the template: `cp animations/_template.html animations/your_name.html`
2. Build your animation using the CSS variable contract for consistent theming
3. Register it in the `ANIMATIONS` array in `index.html`
4. Push — the site updates automatically

See [CONTRIBUTING.md](CONTRIBUTING.md) for the full guide.

## Local development

```bash
python3 -m http.server 8000
```

Then open [http://localhost:8000](http://localhost:8000).

## License

[MIT](LICENSE)
