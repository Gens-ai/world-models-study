# Matrix-Game (Skywork AI, 2025–2026)

**Links**: https://github.com/SkyworkAI/Matrix-Game ,
https://matrix-game-v3.github.io/ , https://huggingface.co/Skywork/Matrix-Game-3.0 ,
arXiv: https://arxiv.org/html/2508.13009 (2.0 paper)

This is the model Joe found first — most actively developed, fully open
source line in the field, now at version 4.0.

## Version history (the interesting part: it's a visible research trajectory)

### Matrix-Game 1.0
Original release — full-sequence (bidirectional) diffusion, fixed-length
generation only. Not real-time.

### Matrix-Game 2.0 (Aug 2025) — "real-time and streaming"
- Built on **Wan I2V** (image-to-video diffusion transformer) foundation model,
  text branch removed, action modules added.
- **Action injection**: continuous mouse movement concatenated into latents →
  MLP → temporal self-attention; discrete keyboard actions via cross-attention
  — frame-level granularity for both.
- Converted the bidirectional foundation model to **autoregressive** via
  "Self-Forcing" distillation: the student model is trained to condition on
  its *own* previously generated frames (not ground truth), which is the fix
  for exposure bias / error accumulation that plagues naive teacher-forcing.
- **Rolling KV-cache**: fixed-length cache of recent latents+actions, evicts
  oldest tokens — enables "infinite-length" generation in principle.
- Scalable **data pipeline built on Unreal Engine** — ~1200 hours of synthetic
  gameplay footage with interaction annotations (keyboard/mouse labeled) —
  solves the same "where does training data come from" problem GameNGen solved
  with an RL agent, but via synthetic engine capture instead.
- Results: 352×640, 25 FPS, minute-level videos. Fully open-sourced
  (weights + code) — first open-source model of its kind at this point.
- **Stated limitations** (their own paper): poor out-of-domain generalization
  (camera moves far in a scene type it wasn't trained on → degraded/over-
  saturated output); resolution below SOTA video models; no explicit memory
  mechanism, so long-video content consistency still degrades.

### Matrix-Game 3.0 — "long-horizon memory"
Directly targets 2.0's #3 limitation: adds **camera-aware memory retrieval and
injection** plus a "multi-segment autoregressive" design for long-horizon
spatiotemporal consistency. (Haven't read the full paper yet — next step.)

### Matrix-Game 4.0 — hybrid engine + neural rendering (the architectural pivot)
Different philosophy from 1.0–3.0: combines an **executable game engine**
(handles gameplay/physics/input — the deterministic, reliable part) with a
**causal video model** that only does streaming neural rendering — turning
low-poly RGB frames into detailed visuals. Three concrete scene models shipped:
Medieval Castle, Ancient Egypt (3rd-person shooting), City Racing (driving).

This mirrors the "hybrid" path in our integration-ideas.md #3 — Skywork
arrived at the same conclusion we floated independently: pure end-to-end
neural generation isn't yet the practical answer; separating logic (engine)
from visuals (neural renderer) is.

## Why this is the best anchor model for us
- Fully open source across versions — the only line here we could realistically
  run, fine-tune, or learn from by reading code, given GPU access.
- Its own version history **is** a mini-history of the field's open problems
  (real-time → memory → engine hybrid), useful as a syllabus in itself.

## Next steps on this note
- Read the Matrix-Game 3.0 paper in full (memory mechanism design)
- Read Matrix-Game 4.0 release notes/paper when available (engine integration
  details — this is the most relevant version for the "hybrid" build path)
