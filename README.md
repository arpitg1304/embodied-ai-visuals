# Embodied AI Visuals

Interactive animations explaining core concepts in robotics and embodied intelligence.

**Live site:** [arpitg1304.github.io/embodied-ai-visuals](https://arpitg1304.github.io/embodied-ai-visuals/)

## Animations

| Animation | Category | Description |
|-----------|----------|-------------|
| VLA Model Explainer | Perception | Step-by-step walkthrough of Vision-Language-Action models — from camera input to robot action output |
| Sim-to-Real Gap Explainer | Learning | Why sim-trained policies fail in the real world and how domain randomization bridges the gap |
| Reward Shaping — Sparse vs Dense | Learning | How reward function design shapes learning — sparse rewards, dense gradients, and potential-based shaping |
| Video Action Models & Latent Space | Learning | How video-conditioned policies use temporal context and latent space predictions to generate robot actions |
| Diffusion Policy | Learning | How denoising diffusion refines random noise into smooth action trajectories, handling multimodal demonstrations |
| Flow Matching | Learning | How flow matching learns straight-line velocity fields to transport noise into action distributions — a faster, simpler alternative to diffusion |

## Features

- **No dependencies** — pure HTML/CSS/JS, zero build step
- **Dark themed** — easy on the eyes
- **Embeddable** — copy iframe embed code for any animation to use in your blog or slides
- **Mobile friendly** — responsive layout that works on any device
- **Auto-deploy** — push to `main` and GitHub Actions deploys to Pages

## Roadmap

Planned animations, roughly ordered by pedagogical flow. Contributions welcome!

### Perception & Representation
- [ ] **Visual Encoders Compared** — CNN vs ViT vs DINOv2: how each architecture turns pixels into features, and why foundation vision models changed robotics
- [ ] **Point Cloud Processing** — From raw depth sensor → voxel grid → PointNet features. Show how 3D understanding feeds into grasp planning
- [ ] **Spatial Action Maps** — How pixel-space affordance maps let robots decide *where* to act directly from images

### Planning & Control
- [ ] **MPC vs Learned Policies** — Model Predictive Control re-plans every step; a learned policy runs open-loop. Animated side-by-side on the same task
- [ ] **Inverse Kinematics Explained** — Given a target end-effector pose, how the robot solves for joint angles — Jacobian, gradient descent, singularities
- [ ] **Task and Motion Planning (TAMP)** — High-level symbolic plan ("pick → place → stack") grounded into continuous motion trajectories
- [ ] **Behavior Trees vs FSMs** — Two paradigms for structuring robot decision-making, animated with a pick-and-place example

### Learning & Adaptation
- [ ] **Imitation Learning Pipeline** — Human demo → trajectory encoding → policy distillation. Show how a few demonstrations become a generalizable skill
- [x] **Diffusion Policy** — Denoising process that iteratively refines random noise into a smooth action trajectory — the key insight behind diffusion-based robot control
- [ ] **Hindsight Experience Replay** — Failed trajectories relabeled with achieved goals — turning failures into training signal
- [ ] **Curriculum Learning for Manipulation** — Progressively harder tasks: reach → touch → grasp → lift → stack

### Multi-Agent & Communication
- [ ] **Multi-Robot Task Allocation** — How a team of robots divides tasks using auction-based or graph-based coordination
- [ ] **Human-Robot Handoff** — Timing, grip force negotiation, and intent prediction during object handovers

### Safety & Deployment
- [ ] **Safe RL with Constraints** — Reward maximization *plus* constraint satisfaction — how robots learn to be both capable and safe
- [ ] **Failure Detection & Recovery** — How robots monitor execution, detect anomalies, and trigger recovery behaviors in real-time

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
