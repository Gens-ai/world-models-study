# Genie 1 / 2 / 3 (Google DeepMind, 2024–2026)

**Links**: https://deepmind.google/blog/genie-3-a-new-frontier-for-world-models/,
https://blog.google/innovation-and-ai/models-and-research/google-deepmind/project-genie/

## What it is
DeepMind's flagship world-model line, explicitly framed as an AGI building
block (training ground for embodied agents), not just a game demo. Genie 1/2
generated environments for agents to act in; **Genie 3** (Aug 2025) is the
first version with real-time interactivity and now ships as a consumer
product ("Project Genie", Jan 2026, gated to Google AI Ultra subscribers).

## Capabilities (Genie 3)
- **Text-to-world**: a text prompt generates a navigable 3D-feeling world.
- Real-time navigation at 24 FPS, 720p.
- **World memory**: consistency for "several minutes", with visual memory
  reaching back ~1 minute — notably better than GameNGen/Oasis, and DeepMind
  calls this an *emergent* capability (not an explicit 3D representation like
  NeRF/Gaussian Splatting — it's learned purely from frame-by-frame generation).
- **Promptable world events**: mid-session text commands can alter the world
  (change weather, add objects/characters) — a distinct interaction channel
  from navigation.
- Used to generate worlds for **SIMA** (DeepMind's generalist 3D agent) to test
  agent compatibility — the agent sends navigation actions, Genie 3 simulates
  consequences, Genie doesn't know the agent's goal.

## Architecture
Not disclosed in detail (no open paper on internals) — treat as a black box,
closed weights, closed inference.

## Limitations (as stated)
- Action space still limited — promptable events aren't actions the *agent*
  itself performs, just environmental interventions.
- Can't simulate real-world locations with geographic accuracy.
- Text rendering inside the world is unreliable.
- A few minutes max continuous interaction, not hours.
- No modeling yet of multiple independent agents interacting with each other.

## Why it matters most for "agent integration"
Genie/SIMA is the closest existing precedent for exactly the integration angle
Joe's interested in: agent issues actions → world model renders consequences
→ agent perceives and acts again. DeepMind's own gap analysis ("agents lack
high-level reasoning to alter the simulation themselves") is the open problem
our own integration ideas should aim at.

## Access
Closed. No API/self-host path — only through Project Genie UI for AI Ultra
subscribers in the US. Not something we can build on directly today.
