---
title: Low-Rank Quantization-Aware Training for LLMs
tags:
  - LLM
  - QAT
  - Compression
  - Paper
draft: true
---

## Low-Rank Adaptation (LoRA)

$$
\mathbf y = \boldsymbol{W_0} \mathbf x + \frac{\alpha}{r}\boldsymbol{AB}\mathbf{x}\\
=\left(\mathbf{W_0}+ \frac{\alpha}{r}\boldsymbol{AB}\right)\mathbf x
$$
## Motivation

- Use PEFT to make QAT more memory- and runtime-efficient.
- Design LoRA to also allow efficiency during inference time, i.e. ensuring that LoRA modules can be merged into the quantized weights.

## Methodology

- Weight quantization formulation

$$
\widehat{\boldsymbol{W}} := \mathbf{s} \cdot \text{clip}\left(\left\lfloor \frac{\boldsymbol W}{\mathbf{s}} \right\rceil, -2^{b - 1}, 2^{b - 1} - 1  \right)
$$

- Place the LoRA module inside the quantization function (`clip`) to prevent accuracy loss.

$$
\widehat{\boldsymbol{W}} := \mathbf{s} \cdot \text{clip}\left(\left\lfloor \frac{\boldsymbol W_0}{\mathbf{s}} + \frac{\alpha}{r}\boldsymbol{AB}\right\rceil, -2^{b - 1}, 2^{b - 1} - 1  \right)
$$

- Divide the frozen weight by the initial scale instead of the trainable scale and store it in a low-precision format.

$$
\begin{gather}
\widehat{\boldsymbol{W}} := \mathbf{s} \cdot \text{clip}\left(\left\lfloor \frac{\boldsymbol W_0}{\mathbf{s_0}} + \frac{\alpha}{r}\boldsymbol{AB}\right\rceil, -2^{b - 1}, 2^{b - 1} - 1  \right)\\
\boldsymbol{\Phi_0} := \varphi\left(\frac{\boldsymbol{W_0}}{\mathbf{s_0}}\right)
\end{gather}
$$

- Handle 
- Initialize LoRA weights $\boldsymbol{A}, \boldsymbol{B}$
