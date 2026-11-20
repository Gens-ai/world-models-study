# Hosted Services — No Code, No GPU

Services you can go prompt a custom world right now, zero setup. Checked
2026-11-20.

## 1. Oasis 3 Preview (Decart) — free, no signup, try this first
**https://oasis3-preview.decart.ai**
- Playable in-browser immediately, no API key needed for the web demo.
- Text-prompt a scene (driving-focused — presets like "misty forest canyon",
  "rainy downtown night"), then drive it live with keyboard.
- Real-time: ~22 FPS, <200ms latency, 512x768 resolution.
- Note: Decart's actual product direction has shifted to **robotics/AV
  simulation infra** (https://decart.ai/oasis — "Oasis 3" is now pitched as
  closed-loop training infra for autonomous vehicles, API-accessible via
  gRPC/Python SDK `decart-oasis` with a paid `DECART_API_KEY`). The free web
  demo at oasis3-preview.decart.ai is the no-cost leftover of that pivot.
- Also: https://oasis2.decart.ai — their earlier gaming-flavored version
  ("Gaming, Reimagined Live").

## 2. Project Genie w/ Genie 4 (Google DeepMind) — most impressive, paid
**https://labs.google/projectgenie**
- Just updated Nov 18, 2026 to **Genie 4**: prompt text/image, walk around in
  real time, mid-session prompt edits (change weather, drop in a character,
  redirect the action), now with real-time adaptive native audio
  (ambient sound + character dialogue).
- Genie 3 still selectable for longer sessions (up to 3 min, up from 60s) and
  360-degree panorama-seeded worlds.
- New "Project Genie agent": describe a vision in natural language, it
  orchestrates Google's models to set up the world + soundtrack, then Gemini
  can watch your session and suggest/trigger events.
- Community gallery to explore/remix published worlds.
- **Access**: Google AI Ultra subscribers only (18+, sign in with Google
  Account). AI Pro members can join a waitlist — not immediate access.
- **Pricing** (US, as of May 2026 I/O update): AI Ultra comes in two tiers —
  **$99.99/mo** (5x Pro usage limits) and **$199.99/mo** (20x Pro limits,
  reduced from $250). Project Genie specifically requires the **$200/mo
  tier** — the $100 tier does not include it (confirmed in Google's I/O 2026
  announcement: "Project Genie (AI Ultra $200; global)").
- Available in 140+ countries, must be 18+.

## 3. Marble (World Labs) — persistent 3D worlds, not gameplay, has a free tier
**https://marble.worldlabs.ai** (docs: https://docs.worldlabs.ai)
- Different flavor from the two above: generates a **persistent, exportable
  3D world** (Gaussian splats, textured mesh, or video flythrough) rather
  than a live playable video stream. No physics/character/gameplay — more
  "walk a camera through a generated 3D scene," but you get real geometry
  out the other end.
- Input flexibility: text, single image, multiple images, 360° panorama,
  video, or "Chisel" (block out coarse 3D structure yourself, let Marble
  style it).
- Editing: "Pano edit" (prompt-driven targeted edits), click-to-expand
  (grow the world beyond its original bounds), variations, and "Compose"
  (stitch multiple generated worlds into one larger space).
- Export formats: Gaussian splats (view in-browser via their open-source
  `Spark` renderer, Three.js-integrated), triangle meshes (collider +
  high-quality), usable in Blender/Maya/3ds Max/game engines, or raw video.
- A separate **World API** (Jan 2026) exposes this programmatically for
  developers — but note **Marble app credits and World API credits are
  separate, non-interchangeable balances**, even under the same login.
- **Pricing** — credit-based, 4 tiers (checked 2026-11-16):
  | Plan | Price/mo | Credits | ~Generations | Notable unlocks |
  |---|---|---|---|---|
  | Free | $0 | 7,000 | ~4 | Text/image/panorama input only |
  | Standard | $20 | 20,000 | ~12 | Video input, editing, splat export |
  | Pro | $35 | 40,000 | ~25 | Expand worlds, high-res mesh export, **commercial rights** |
  | Max | $95 | 120,000 | ~75 | High-volume production |
  - A basic single-image world generation costs ~1,580 credits (1,500
    generation + 80 input) — so even the Free plan's 4 generations are a
    real way to try it with zero cost.
  - Top-up credit packs ($5/5k, $20/22k, $50/63k) require a paid plan.

## Recommendation
- **Try first, zero cost**: Oasis 3 Preview — immediate, playable, no account.
- **If you want something exportable to actually build with**: Marble Free
  tier (4 generations, no card needed) — closest match to "start building
  worlds" since the output is real 3D geometry, not just a video stream.
- **If budget allows and you want the frontier experience**: Project Genie
  needs the $200/mo AI Ultra tier specifically — steep for a side study;
  revisit once/if the broader "building worlds" direction firms up.
