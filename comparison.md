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

## Models to add next
- DIAMOND (diffusion world model for RL, Atari/CSGO)
- UniSim (Google, "universal simulator")
- WorldDreamer
- Genie 2 (predecessor, worth the delta vs. 3)
- Mineworld
