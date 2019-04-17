---
layout: post
title:  "Compare l1 and l2 regularizaion."
date:   2019-02-10 20:50:45 +0800
categories: yuehan notes
---

In this artical, we explain why l1 regularization causes sparse parameters, but l2 regularization can not.
Let's suppose the cost functions of weights in terms of l1 and l2 regularization are 

$$L_1(w) = J(w)+\sum_{i=1} |w_i|$$

and

$$L_2(w) = J(w)+\sum_{i=1} (w_i)^2.$$

We apply gradient descent to update $w_i$, which means

$$w_i =  w_i-\alpha\cdot\frac{\delta L_1}{\delta w_i}\\
	= w_i-\frac{\delta J(w)}{\delta w}-sgn(w_i)
$$ for l1 reg,

$$w_i =  w_i-\alpha\cdot\frac{\delta L_1}{\delta w_i}\\
	= w_i-\frac{\delta J(w)}{\delta w}-2(w_i)
$$for l2 reg.

Note that sgn represents signal function. Above shows that when $w\in(1,+\infty)$, $w_i$ of l2 decreases faster than that og l1 reg. When $w$ becomes less than 1 and approximates 0, $w_i$ for l2 decreases extremely slowly, while $w_i$ for l1 maintains a constant decreasing velocity. Thus if we keep training under l1 reg, many of $w$ will become zero ultimately.
