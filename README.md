# DiffiT: Diffusion Vision Transformers for Image Generation

## Introduction
In this project I propose an implementation and possible lightweight variants of DiffiT, a paper from NVidia Labs published in 2023 [DiffiT: Diffusion Vision Transformers for Image Generation](https://arxiv.org/abs/2312.02139) that achieve the SOTA result if image generation using a diffusion model with Vision Transformers (ViTs) introducing a novel feature: the Time-Dependent Multi-Head Self-Attention mechanism. DiffiT achieves a new SOTA FID score of 1.73 on ImageNet-256 dataset !

In this implementation I also present a possible lightweight version of the architecture using Depthwise Separable Convolutions and MetaFormers (in particular PoolFormers). The former allows us to decrease the high number of parameters of the architecture without losing so much in accuracy, while the latter is a way to decrease the "high demanding resources" problem of the transformer architecture.

![teaser_main](https://github.com/damianoimola/diffit/assets/45452420/e226e4e9-5eb3-4e37-b902-8f6a22988ff1)



## Diffusion models
Diffusion models, have emerged as a powerful class of probabilistic models for generating complex data distributions. These models operate by simulating the diffusion process, wherein data is gradually transformed into noise through a series of stochastic steps. The generative process is then the reverse of this diffusion, starting from pure noise and gradually refining the data to approximate the original distribution. The foundational concept of diffusion models can be traced to the field of physics, particularly the study of thermodynamic processes where systems evolve over time towards equilibrium.




## Vision Tansformers (ViTs)
Vision Transformers (ViTs) the transformative power of the Transformer architecture originally designed for natural language processing. Unlike traditional convolutional neural networks (CNNs), which have dominated the vision landscape for decades (and are still quite used for a variety of tasks, especially involving low resources architectures), Vision Transformers utilize self-attention mechanisms to model the global relationships between different parts of <ins>the same<ins> image.






## DiffiT novelty
This novel introduction allows the transformer to gather spatio-temporal informations regarding input data, thanks to its time dependency. Let $x_s$ and $x_t$ respectively the spatial and temporal embeddings. The attention module's Query, Key and Values are defined as follows:

$$
\begin{align}
q_s = x_s W_{qs} + x_t W_{qt}\\
k_s = x_s W_{ks} + x_t W_{kt}\\
v_s = x_s W_{vs} + x_t W_{vt}\\
\end{align}
$$

where $W_{qs}, W_{qt}, W_{ks}, W_{kt}, W_{vs}$ and $W_{vt}$ denote spatial (i.e. the ones with subscript $\_{*s}$) and temporal (i.e. the ones with subscript $\_{*t}$) projection weights for their corresponding queries, keys, and values respectively.\

The initial equations listed above are equivalent to linear projection of each spatial token concatenated with linear projection of each time token. As a result, **Query, Key and Values** are are all **linear functions** of both time and spatial tokens.

This is a really good thing, since in this way, Query, Key and Values can modify their behavious adaptively according to the timestep!\
In other words, *attention module can learn to act differently based on the timestep in which diffusion process is* 🙂.
