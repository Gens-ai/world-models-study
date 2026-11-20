# World Models Study

Learning notes on **interactive neural world models** — AI systems that generate
playable/navigable video in real time, conditioned on user actions, aiming to
replace or augment traditional game engines. Goal: survey the field, then move
toward building something.

## Status
Survey/literature phase. No code run yet — most of these models need real GPU
hardware (H100-class) to run, which isn't available on theforest today.

## The core idea across all these models
Instead of a hand-coded engine (physics, renderer, game logic), a generative
model (usually diffusion or autoregressive-transformer based) predicts "what
the next frame looks like" given the previous frames + the user's action
(keyboard/mouse/text). The "engine" is learned, not programmed.

## Index
- [comparison.md](comparison.md) — side-by-side matrix across models
- [integration-ideas.md](integration-ideas.md) — ideas for combining world
  models with agent systems, and a path toward actually building
- `notebooks/` — one deep-dive note per model

| Model | Org | Year | Notes |
|---|---|---|---|
| [GameNGen](notebooks/gamengen.md) | Google Research/DeepMind | 2024 | First "diffusion model as real-time game engine" (Doom) |
| [Oasis](notebooks/oasis.md) | Decart + Etched | 2024 | Real-time Minecraft-like, open weights (500M) |
| [Genie 1/2/3](notebooks/genie.md) | Google DeepMind | 2024–2026 | Text-to-world, general purpose, now a product (Project Genie) |
| [Matrix-Game](notebooks/matrix-game.md) | Skywork AI | 2025–2026 | Open-source, 1.0→4.0, now hybrid engine+neural rendering |

## Why this matters / where it's headed
- **Game dev**: prototyping worlds without building a renderer/engine
- **RL/robotics**: cheap, infinite simulators for training agents (this is
  DeepMind's explicit AGI angle with Genie/SIMA)
- **New medium**: "worlds" as a generated, explorable artifact distinct from
  both video and games
