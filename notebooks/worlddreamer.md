# WorldDreamer (Jeff Wang et al., Jan 2024)

**Links**: https://world-dreamer.github.io/ , https://github.com/JeffWang987/WorldDreamer
**Paper**: "WorldDreamer: Towards General World Models for Video Generation via Predicting Masked Tokens" (arXiv 2401.09985)

## What it is
A third architectural family, distinct from both diffusion (Oasis, DIAMOND,
Matrix-Game) and plain autoregressive-token models: **masked visual token
prediction**, borrowing the "BERT-style" masking idea instead of next-token
or denoising. Targets general video generation (natural scenes + driving),
not specifically games.

## Architecture
- **VQGAN** tokenizes frames into discrete visual tokens (vocab size 8192,
  16x spatial downsample).
- Text (T5 embeddings) and action (MLP embeddings) are concatenated into
  "multimodal prompt" embeddings.
- **STPT** (Spatial-Temporal Patchwise Transformer): processes masked visual
  tokens with spatial-temporal self-attention within patches, then
  spatial-wise cross-attention against the multimodal prompt, predicting the
  masked tokens (cross-entropy loss, not diffusion/regression loss).
- Dynamic cosine mask-rate scheduling during training (same token mask shared
  across all frames in a clip, since adjacent frames are similar — avoids
  information leakage).
- Inference: parallel decoding of masked tokens in ~10 steps total — claimed
  3-20x faster than diffusion (~30 steps) or autoregressive (~200 steps)
  methods for a given clip. 24 frames @ 192x320 in 3 seconds on an A800.

## Why it's worth knowing
Not a real-time interactive demo like Oasis/Matrix-Game — it's a *speed*
argument: masked-token parallel decoding is a third axis (alongside
diffusion-step-count and transformer size) for getting world-model inference
fast enough to be interactive. If diffusion-step-reduction (DIAMOND's
3-step, Matrix-Game's few-step distillation) hits a wall, masked-token
decoding is the alternative lane to watch.

## Limitations / caveats
Older (Jan 2024, pre-dates the interactive real-time wave of Oasis/GameNGen);
demonstrated on text-to-video/image-to-video/video-editing/action-to-video
(driving) tasks, not shown as a live playable game loop the way the others
are. Treat as an architecture-family data point, not a candidate to run.

## Relevance to integration ideas
Low priority for hands-on use; useful mainly as the comparison point proving
"diffusion" isn't the only path to fast world-model inference — relevant if
we ever hit diffusion speed limits during the hybrid-build experiments.
