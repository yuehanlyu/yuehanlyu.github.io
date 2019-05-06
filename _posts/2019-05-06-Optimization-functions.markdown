---
layout: post
title:  "Optimization functions"
date:   2019-05-06 08:50:45 +0800
categories: yuehan notes
---
Let's start from the most often seen ones.
Most authors say that if you don't know which one to use, then use Adagrad.

## Gradient descent

The updating function is
$$\theta_{t+1,i}=\theta_{t,i}-\eta\cdot g_{t,i}$$

|	  |  S-GD    |   mini batch-GD   |  batch-GD    |
| --- | ---- | ---- | ---- |
| speed    | fast     | moderate     |  slow    |
|  convergence of loss |  easy to stuck in local-minimum    | moderate     |  overall minimum    |

Features are updated at the same rate.
But we are eager to update more for rarely accuring feature.

## Momentum
- accelerate SGD in the relevant direction
- dampen oscillations

$$v_t=\mu v_{t-1}+\eta \cdot g_{t,i}\\
\theta = \theta-v_t$$

$v$ represents the descent direction of last time.

## (Adagrad) Adaptive gradient descent

Adopt the learning rate to the parameters.
Suitable for sparse data.(Thus parameters are updated in different rate.)

$$\theta_{t+1,i}=\theta_{t,i} - \frac{\eta}{\sqrt{G_{t,ii}+\epsilon}}\cdot g_{t,i}$$

$G\in \mathbb{R}^{d\times d}$, diagonal element $i,i$ is the sum of the squares of the gradient w.r.t $\theta_i$, up to time step $t$.

## (Adam) Adaptive Momentum Estimation

Adagrad+Momentum.

