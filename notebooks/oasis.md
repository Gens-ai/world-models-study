# Oasis (Decart + Etched, Oct 2024)

**Links**: https://oasis-model.github.io/ , https://oasis.decart.ai

## What it is
"A Universe in a Transformer" — first open-weights, real-time, interactive
world model; a playable Minecraft-like demo with no underlying game code at
all, pitched partly as a showcase for Etched's upcoming Sohu AI ASIC.

## Architecture
- ViT-based spatial autoencoder + DiT (diffusion transformer) backbone — both
  Transformer-based by design choice, explicitly to get stable scaling and
  fast inference on custom silicon (Sohu), unlike GameNGen/DIAMOND's non-
  transformer choices.
- Autoregressive generation, each frame conditioned on keyboard input.
- Trained with **Diffusion Forcing**: independent per-token noise levels,
  enabling novel decoding schemes.
- Key trick for stability: **dynamic noising schedule** at inference — inject
  more noise early in the denoising passes (reduces error accumulation),
  gradually remove it later (lets the model lock in high-frequency detail
  from previous frames). Model saw noise during training so it's robust to it.
- 460p @ 20 FPS on H100s; open-sourced a 500M parameter model + inference code
  (a larger checkpoint only available via hosted demo).

## Why it mattered
- First **open-weights** real-time world model anyone could run locally.
- Explicit commercial/hardware angle: positioned as the "killer demo" that
  justifies building a dedicated inference chip (Sohu) for generative video.

## Limitations (as stated)
- Rough edges reviewers hit immediately: forgets layout when you turn around,
  low resolution, only playable for a few minutes, imprecise inventory/object
  control, fuzzy details at a distance.
- Legal ambiguity: trained on Minecraft footage without Microsoft's blessing
  (explicitly called out by TechCrunch) — worth remembering if we ever train
  on footage of someone else's game/IP.

## Relevance to our integration ideas
It's the most approachable model to actually *run* ourselves (small, open,
documented) if/when we rent a GPU — good first hands-on experiment once the
survey phase is done.
