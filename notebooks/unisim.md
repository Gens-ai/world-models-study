# UniSim (Google DeepMind, ICLR 2024)

**Paper**: "Learning Interactive Real-World Simulators"
**Links**: https://universal-simulator.github.io/ ,
https://deepmind.google/research/publications/47545/

## What it is
Different genre from the others: not a game world model, a **real-world**
action-conditioned video simulator. Given an image and a natural-language
action ("move to x,y location", "open the drawer"), it generates the video of
that action's consequence. Trained by combining many disparate datasets
(robot manipulation footage, driving footage, human activity video, navigation
data, etc.) — each contributes a different aspect of "how the real world
responds to actions."

## Why it's the odd one out in this survey
Everything else here targets games (Minecraft, Doom, CS:GO, generic game
scenes). UniSim targets **real-world embodied actions** — the explicit goal
is training robotics/embodied-agent policies (vision-language planners and
low-level controllers) inside the simulator before deploying to real
hardware, i.e. sim-to-real via generative video instead of a physics engine
like MuJoCo/Isaac.

## Architecture
Generative video model conditioned on a starting image + natural-language
action description, trained across heterogeneous real-world datasets rather
than one domain's gameplay footage. (Less detail published on exact
architecture vs. the game-focused models — treat as a closed/under-specified
system for now, revisit if DeepMind publishes more.)

## Relevance to our integration ideas
Interesting contrast case for integration-ideas.md: this is a world model
built **specifically to be driven by agents/policies**, not humans with a
keyboard — the natural-language action interface is closer to what an LLM
agent would actually emit than keyboard/mouse inputs are. If we ever want an
LLM agent to control a generated world via language rather than translating
to keypresses, UniSim's interface design (not weights — likely not open) is
the reference pattern worth re-reading.

## Access
No indication weights are open/available for self-hosting — treat as a
research paper to learn the *idea* from (language-conditioned real-world
simulation), not a model to run.
