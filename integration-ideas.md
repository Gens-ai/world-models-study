# Integration Ideas — World Models + Agent Systems

Brainstorm, not commitments. Revisit after finishing the survey pass.

## 1. World model as an RL/agent training simulator
This is literally what GameNGen and Genie/SIMA already demonstrate: an agent
acts inside the generated world, the model renders the consequence, no real
engine needed. For us: could be a cheap way to spin up a test environment for
any agent-training experiment without building/licensing a game engine.
Blocker: needs serious GPU (H100-class) to run any of these at interactive
speed — not something we can self-host cheaply today.

## 2. Agent-directed world generation ("LLM as world director")
An LLM agent holds the high-level goal/narrative state, issues prompts or
"promptable world events" (Genie 3's term) to steer the world model, which
renders the playable result. The agent is the game designer; the world model
is the renderer+engine. This is the most buildable angle today since it only
needs API access to a hosted world model (if/when one offers an API) rather
than running the weights ourselves.

## 3. Hybrid engine + neural rendering (the Matrix-Game 4.0 pattern)
Keep a real, cheap, deterministic engine (game logic/physics — something we
can actually build, e.g. a simple Godot/Unity/custom sim) and use a neural
model only for the final visual layer (low-poly → photoreal). This is the
most practically buildable path for "starting to build worlds" without
needing a frontier-scale generative model, and it sidesteps the memory/
consistency problem since the engine is the source of truth.

## 4. Synthetic data / content generation
Use a world model to generate training data for other vision or robotics
models (what GameNGen's RL-agent-recording approach is in miniature, and what
UniSim-style models target). Lower relevance to current projects, parked.

## Path toward "I want to start building worlds" (Joe's stated goal)
Given no GPU access and closed/gated frontier models (Genie 3), the realistic
on-ramp is:
1. **Start with #3 (hybrid)** — build a small interactive scene in a real
   engine (something scriptable/cheap, e.g. a browser-based 3D toy or simple
   Godot project), since that's buildable today with zero exotic hardware.
2. **Experiment with Matrix-Game's open weights** (2.0/3.0) once/if we get
   GPU access (rentable cloud GPU, e.g. RunPod/Vast.ai hourly H100) — it's the
   only frontier-adjacent model that's actually open source end-to-end.
3. **Layer in an agent** once there's a working loop to direct — e.g. an LLM
   agent that edits the Godot scene or issues actions, start text-only before
   trying to wire up a neural renderer.

Revisit this doc once the survey (comparison.md) covers 6+ models.
