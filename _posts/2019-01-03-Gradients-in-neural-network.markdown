---
layout: post
title:  "Compute gradients in neural network."
date:   2019-01-03 13:57:45 +0800
categories: yuehan notes
---
How neural network update weights of its hidden units? This blog mainly refers from Andrew Ng's course [Deep learning][Andrew-dl].
# Do the prediction
Suppose we are constructing the simplest neural network that only has 1 layer of hidden neurons. It can be regarded as a logistic regression model. For one sample, given weights, we first compute the predicted $\bar{y}$, and the logloss $L$ caused by error between it and ground true:

$$z=w_1x_1+w_2x_2+b\\
\bar{y}=\sigma(z) = \frac{1}{1+e^{-z}}\\
L(\bar{y},y)=(1-y)log(\frac{1}{1-\bar{y}})+ylog(\frac{1}{\bar{y}})$$

# Compute gradients to update weights
Hereto, $L$ shows the perforance of $w_1, w_2, b$, so we updates those weights(parameters) accordingly. We use gradient descent to update those parameters. Here is a general form of gradient descent, taking updating $w_1$ for instance:

$$
w_{1,t+1}=w_{1,t}-\alpha \frac{\delta L}{\delta w_{1,t}},
$$

The $\alpha$ here is learning rate. So we have to compute $\frac{\delta L}{\delta w_1,t}$, we simply note it $\delta w_1$.
According to chain rule,

$$\delta w_1=x_1\cdot \frac{\delta L}{\delta z}\\
=x_1\cdot\frac{\delta L}{\delta \bar{y}}\cdot \frac{\delta \bar{y}}{\delta z}\\
=x_1\cdot (y-\bar{y})$$

When we have $m$ examples, we just sum them up to obtain $\frac{1}{m}\sum_{i=1}^m\delta w_1^{(i)}$, because $L$ summing up across all samples is additive. 

# Back propagation
In the previous example, we only have one layer of weights to update. In a deeper network, the formula of $\delta w_1$ will incorptes weights of latter layers. In this case, we first update those latter weights (in terms of layer index), then update $w_1$, following the same methodology. This procedure is called back propagation.

Back propagation leads to two problems regarding gradients. They are `gradient vanishing` and `gradient explosion`. We will talk about using different activation funciton to solve those two problems in another blog.


[Andrew-dl]: https://www.coursera.org/learn/neural-networks-deep-learning/home/week/3
