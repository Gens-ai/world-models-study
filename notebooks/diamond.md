# DIAMOND (Eloi Alonso et al., NeurIPS 2024)

**Links**: https://diamond-wm.github.io/ , https://github.com/eloialonso/diamond
**Paper**: "Diffusion for World Modeling: Visual Details Matter in Atari" (DIffusion As a Model Of eNvironment Dreams)

## What it is
A diffusion world model built primarily as an **RL research tool**, not a demo:
train an RL agent entirely "in imagination" inside the diffusion model, never
touching the real environment except to collect more data. Also separately
shown to work as a standalone interactive engine (CS:GO), with no RL agent at
all — just a human playing inside the generated world.

## Architecture
- Standard 2D U-Net (not a transformer/DiT like the others) predicting the
  denoising vector field.
- Conditions on past frames by **channel-concatenation** (stack L past
  observations+noisy next observation), and on actions via **adaptive group
  norm** layers inside the U-Net's residual blocks — notably simpler
  conditioning than Matrix-Game's cross-attention approach.
- Separate reward/termination model (CNN+LSTM) needed to make the diffusion
  model usable as a full RL training environment.
- **Atari**: tiny — 4M parameters, 12GB VRAM, ~2.9 days on an RTX 4090 per
  game/seed.
- **CS:GO**: scaled up to 381M params (including a 51M-param upsampler
  diffusion model to go from low-res 56x30 to higher res). Trained on 5.5M
  frames / 87 hours of Dust II gameplay, 12 days on an RTX 4090.
- Only needs **3 denoising steps** for the dynamics model (vs. ~30 typical) —
  runs the CS:GO model at **10Hz on an RTX 3090**.

## Results
- Atari 100k benchmark: mean human-normalized score 1.46 — best-ever for an
  agent trained *entirely* inside a world model (beats DreamerV3, IRIS, STORM,
  TWM, SimPLe baselines).
- CS:GO: stable trajectories over hundreds of timesteps, but drifts
  out-of-distribution in less-visited map areas; approaching walls or losing
  visibility can make it forget state and hallucinate a new area/weapon.
  Also wrongly generalized "jump" into allowing illegal mid-air double-jumps
  — a nice concrete example of a diffusion world model learning a *wrong*
  physical rule because the training data didn't disambiguate it.

## Why it's the most relevant one for us, hardware-wise
**This is the one actually validated on consumer GPUs we might own** — RTX
3090/4090, explicitly, not H100s. The CS:GO model (381M, 10Hz on a 3090) is
in the same hardware class as Joe's 3080. Worth checking first, before Oasis,
as the most likely "can I actually run this at home" candidate — fully open
code+weights+training scripts on GitHub, smaller and better-documented than
Matrix-Game.

## Relevance to integration ideas
This is the strongest real-world precedent for "RL agent trained purely
inside a generated world" — if we ever want to train any agent against a
simulated environment, DIAMOND's actor-critic-in-imagination loop
(Section 3.2 of the paper) is the concrete algorithm to copy, not Genie/SIMA's
closed black box.
