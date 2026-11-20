# GameNGen (Google Research / DeepMind, Aug 2024)

**Paper**: "Diffusion Models Are Real-Time Game Engines"
**Links**: https://gamengen.github.io/index.html

## What it is
First demonstration that a neural model (no hand-coded engine at all) can run
a known, complex game — DOOM — interactively, in real time, at playable
quality.

## Architecture
- Two-phase training:
  1. Train an **RL agent** to play DOOM; record its (action, frame) trajectories
     at scale (~900M frames) — solves the "we can't collect this much human
     gameplay" problem.
  2. Fine-tune **Stable Diffusion v1.4** to predict the next frame, conditioned
     on the sequence of past frames + actions.
- **Noise augmentation on context frames** during training — critical trick:
  corrupting past frames with Gaussian noise during training teaches the model
  to self-correct, which prevents autoregressive drift (errors compounding
  frame over frame) at inference.
- Fine-tuned just the VAE decoder (not the full autoencoder) with MSE loss
  against pixels, to fix HUD/detail artifacts from the pretrained SD autoencoder.
- Runs at >20 FPS on a single TPU.

## Why it mattered
Proved the core thesis of this whole field: you can replace a hand-coded game
engine with a generative video model and get something genuinely playable.
Became the reference point every later model (Oasis, Matrix-Game) positions
itself against.

## Limitations (as stated)
- Only ~3 seconds of context/memory — revisiting a location means the model is
  guessing, not recalling.
- Tailored to one specific, closed game (DOOM) — not shown to generalize.
- Not open source (research paper/demo only).

## Relevance to our integration ideas
The RL-agent-for-data-collection trick is reusable: if we ever want training
data for a world model of our own domain, "train an agent to play/explore it,
record trajectories" is a cheaper path than collecting human demonstrations.
