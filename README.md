# DiffiT: Diffusion Vision Transformers for Image Generation

## Introduction
In this project I propose an implementation and possible lightweight variants of DiffiT, a paper from NVidia Labs published in 2023 [DiffiT: Diffusion Vision Transformers for Image Generation](https://arxiv.org/abs/2312.02139) that achieve the SOTA result if image generation using a diffusion model with Vision Transformers (ViTs) introducing a novel feature: the Time-Dependent Multi-Head Self-Attention mechanism.

This novel introduction provides to the self-attention mechanism also a learnable time-dependent parameter, so that it can encode in this token additional information about the actual timestep.
