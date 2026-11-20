# Comparison Matrix

| Axis | GameNGen (Google, 2024) | Oasis (Decart/Etched, 2024) | Genie 3 (DeepMind, 2025) | Matrix-Game 2.0/3.0/4.0 (Skywork, 2025–26) |
|---|---|---|---|---|
| **Architecture** | Diffusion (fine-tuned Stable Diffusion v1.4), autoregressive on past frames+actions | ViT autoencoder + DiT backbone, autoregressive, trained w/ Diffusion Forcing | Autoregressive world model (architecture undisclosed in detail), text+action conditioned | DiT (built on Wan I2V), action modules injected via cross-attn (keyboard) + concat (mouse); 4.0 adds an actual executable engine for game logic |
| **Conditioning** | Discrete game actions (from RL agent) | Keyboard input | Text prompt to create world; keyboard/mouse to navigate; "promptable world events" to edit it live | Frame-level keyboard (discrete) + mouse (continuous) actions |
| **Real-time / FPS** | >20 FPS on a single TPU | 20 FPS on H100 | 24 FPS, 720p | 25 FPS (2.0), "minute-level" long video |
| **Memory/consistency horizon** | ~3 sec of context (explicitly noted limitation) | Short — "quickly forgets layout", limited memory | Several minutes, ~1 min visual memory lookback | 2.0: no explicit memory (noted limitation); 3.0 adds "camera-aware memory retrieval" for long-horizon consistency |
| **Open weights/code** | No (research paper only) | **Yes** — 500M model + inference code open | No — closed, gated access (Project Genie, AI Ultra only) | **Yes** — fully open-source, HF weights for 2.0/3.0 |
| **Training data** | RL agent self-play recordings (~900M frames) of Doom | Millions of hours Minecraft gameplay + actions | Proprietary, large-scale, diverse (text-to-world) | ~1200 hrs synthetic Unreal Engine + gaming footage with interaction annotations (custom data pipeline) |
| **Game logic / physics** | Entirely learned, no explicit engine | Entirely learned, no explicit engine | Entirely learned, no explicit engine ("no physics engine") | 2.0/3.0: entirely learned; **4.0 is the outlier** — explicit executable engine handles game logic/physics, neural model only does rendering (low-poly → photoreal) |
| **Target game/domain** | Doom specifically (closed domain) | Minecraft-like (open-ended within that aesthetic) | General purpose — any described world | General game scenes; 4.0 ships 3 concrete scenes (medieval castle, Ancient Egypt, city racing) |
| **Stated purpose** | Prove feasibility of "engine-free" real-time games | Consumer demo / proof of concept, hardware showcase for Sohu ASIC | AGI research — training ground for embodied agents (SIMA), now also a consumer creative product | Research + open benchmark for the field; practical push toward engine+model hybrids |

## Key axis to track as the field evolves
**Memory/consistency horizon** is the single biggest differentiator and the
active research frontier — every model above lists "forgets the world after
N seconds/minutes" as its top limitation. Watch for whoever solves long-horizon
memory first (explicit scene representation vs. learned implicit memory).

**Pure-neural vs. hybrid** is the other fork in the road: Matrix-Game 4.0
abandoning "100% neural" for an engine+neural-rendering hybrid is a signal that
fully-learned physics/logic may not be the practical end state — worth
revisiting as more labs follow or don't follow this pattern.

## Second table: RL-focused, alt-architecture, and real-world models

These don't fit the "flagship real-time demo" framing of the table above —
different goals (RL research, non-game domains) or different architecture
families (plain autoregressive transformer, masked-token). Kept separate
rather than cramming a 9-column table.

| Axis | DIAMOND (2024) | MineWorld (Microsoft, 2025) | Genie 2 (DeepMind, 2024) | UniSim (DeepMind, 2024) | WorldDreamer (2024) |
|---|---|---|---|---|---|
| **Architecture** | 2D U-Net diffusion, action via adaptive group norm | Pure autoregressive Transformer + "Diagonal Decoding" for parallel speed (no diffusion) | Autoregressive latent diffusion, causal-masked transformer dynamics | Generative video model, language-conditioned actions (architecture under-specified) | VQGAN tokenizer + masked visual-token prediction (STPT transformer) |
| **Domain** | Atari (26 games) + CS:GO (standalone, no RL) | Minecraft only | General 3D worlds from an image prompt | **Real-world** embodied actions (robots, driving, navigation) — not a game | General video (natural scenes + driving) |
| **FPS / speed** | CS:GO: 10Hz on an RTX 3090 (only 3 denoising steps) | 4-7 FPS (smaller models); ~3 FPS at 1.2B params | Not real-time in published demos (distilled real-time version exists, quality unpublished) | Not real-time — offline video generation | ~10 parallel decode steps; 24 frames @ 192x320 in 3s on an A800 |
| **Open weights/code** | **Yes** — full training+inference code, HF weights, runs on consumer GPUs (3090/4090) | **Yes** (GitHub/HF) — checkpoints reportedly taken down temporarily as of May 2025, verify before relying on it | No — blog demos only | No indication of open weights | **Yes** — GitHub + paper |
| **Consumer-GPU runnable?** | **Yes, validated** — Atari (4M params, 12GB VRAM) and CS:GO (381M params, 3090 at 10Hz) both explicitly run on consumer cards | Likely yes at smaller sizes (not stated, but 4-7 FPS implies modest hardware) | No — closed | No — closed/research only | Needs an A800-class GPU for the stated benchmark, untested smaller |
| **Standout idea** | RL agent trained **entirely inside** the diffusion world model ("in imagination") — best published result for that approach | "Diagonal Decoding" — parallel decoding trick for AR-transformer speed, no diffusion needed | First to show "long-horizon memory" + SIMA-agent-in-the-loop publicly | Language-conditioned (not keyboard) actions — closest interface to how an LLM agent would actually talk to a world model | Masked-token parallel decoding as a 3rd speed strategy, alongside diffusion-step-reduction and AR-transformer tricks |

### Reading the two tables together
- **Most likely to actually run on a 3080**: DIAMOND (both its Atari and
  CS:GO checkpoints are explicitly validated on RTX 3090/4090, same hardware
  class) — try this *before* Oasis.
- **Best "agent talks to world model" interface precedent**: UniSim
  (language actions) and Genie 2/3+SIMA (keyboard/mouse agent-in-the-loop) —
  read both before designing our own agent-integration interface.
- **Speed-without-diffusion alternatives**: MineWorld (AR-transformer +
  Diagonal Decoding) and WorldDreamer (masked-token) — reference if diffusion
  step counts become a bottleneck in our own experiments.

## Models still not covered (future additions)
- Sora / Veo as implicit "world models" (not action-conditioned, but DeepMind
  explicitly cites Veo's physics understanding as a precursor to Genie)
- Any 2026 successors to Matrix-Game 4.0's engine-hybrid approach
