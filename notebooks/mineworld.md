# MineWorld (Microsoft, Apr 2025)

**Links**: https://github.com/microsoft/mineworld , https://huggingface.co/microsoft/mineworld
**Paper**: "MineWorld: a Real-Time and Open-Source Interactive World Model on Minecraft" (arXiv 2504.08388)

## What it is
Open-source, real-time Minecraft world model — directly comparable to Oasis,
but from Microsoft and using a pure autoregressive-transformer approach
(no diffusion at all) plus a novel decoding trick for speed.

## Architecture
- **Visual-action autoregressive Transformer**: takes paired (game scene,
  action) sequences, generates next scenes following actions — token-based,
  not diffusion.
- Key contribution: **"Diagonal Decoding"** — a parallel decoding scheme
  (separate March 2025 paper) that lets the transformer generate frames fast
  enough for real-time play without diffusion's iterative denoising.
- Result: **4-7 FPS** at smaller model sizes; scaling to 1.2B params improves
  image quality but drops to ~3 FPS — a direct, well-documented
  quality-vs-speed tradeoff curve (useful reference point).
- Ships a web demo (Gradio) and local inference code; action list mirrors
  actual Minecraft controls (camera X/Y, movement, interact, etc.) plus a
  "jump to start frame" feature to pick a reference frame from a provided
  scene video.

## Why it matters for the comparison
It's the clearest **head-to-head counterpoint to Oasis**: same domain
(Minecraft), similarly open (weights + code on GitHub/HF), but pure
autoregressive-transformer instead of diffusion, and noticeably slower
(4-7 FPS vs. Oasis's 20 FPS) — concrete evidence that, at least as of 2025,
diffusion-based approaches had a real-time speed edge over naive
autoregressive transformers for this task (though WorldDreamer's and
Matrix-Game's "few-step"/parallel decoding tricks on top of either family
narrow that gap).

## Caveats
- Trained solely on Minecraft; explicitly warns against feeding it non-
  Minecraft images — it will produce incoherent output.
- "The model checkpoints in the Huggingface repo have been temporally taken
  down" (May 2025 news note on the repo) — check current availability before
  planning to actually run it.

## Relevance to our build path
Another open, documented, relatively small model worth checking against
DIAMOND and Oasis for "can my 3080 run this" — lower FPS ceiling than Oasis
but a genuinely different (transformer, not diffusion) codebase to learn from
if we want to understand the autoregressive-token approach hands-on.
