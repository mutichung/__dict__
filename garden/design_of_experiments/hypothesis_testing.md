---
title: Hypothesis Testing
date: 2024-06-10
tags:
  - DoE
draft: true
---

## Introduction
## Comparative Experiments

- Dot diagrams work very well with small samples (20~30).
- Larger samples => histogram.

## The Hypothesis Testing Framework

- Key: sampling from a **normal distribution**.
- Statistical hypotheses
    - $H_0$: null hypothesis. $\mu_1 = \mu_2$.
    - $H_1$: alternate hypothesis. $\mu_1 \neq \mu_2$.

## Two-Sample t-Test

- Test the (null) hypothesis that two populations have equal means.
- How different the sample means are in standard deviation units.
- Assumption:
    - Normal distribution.
    - Doesn't have to be equal variance.
    - Two samples are independent.

$$
\begin{align}
Z_0 &= \frac{\text{Difference in sample means}}{\text{Standard deviation of the difference in sample means}}\\
&= \frac{\bar{y}_1 - \bar{y}_2}{\sqrt{\frac{{\sigma_1}^2}{n_1} + \frac{{\sigma_2}^2}{n_2}}}
\end{align}
$$