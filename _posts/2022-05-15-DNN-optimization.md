---
layout: post
title:  "DNN Optimization"
date:   2022-05-15 17:11:00 +0800
categories: DNN
---

# 优化方法

## GD (Gradient Descent)

$$x_{t+1} = x_t - \eta_t \nabla f(x_t)$$

_优点：_

* 一阶近似方法，计算量小。
* 适用范围广。

_缺点：_

* 容易陷入鞍点或局部最优点。
* 靠近输入层的梯度越来越不稳定可能导致梯度消失或者梯度爆炸。

## SGD (Stochastic Gradient Descent)

$$x_{t+1} = x_t - \eta_t g_t$$

且$E[g_t]=\nabla f(x_t)$

_优点：_

* 不容易陷入鞍点或局部最优值。
* 最终效果通常好于GD。

_缺点：_

* 容易震荡，训练过程比GD通常更长。
* 随机性较大，可解释性差。

_解释性：_

* 当x点的导数比较大，或x点的Hessian矩阵包含一个负的特征值
或x接近（局部）最优，则SGD能找到较好的答案，即strict saddle性质。
* 人们发现大量的机器学习问题，几乎所有的局部最优是几乎一样好的。

_变形：_

**SGD-M (Stochastic Gradient Descent Momentum)**

$$x_{t+1} = x_t - (\gamma m_{t-1} + \eta_t g_t)$$

且$E[g_t]=\nabla f(x_t)$

引入了动量的概念，有效地减少了震荡。

**NAG (Nesterov Accelerated Gradient)**

$$x_{t+1} = x_t - (\gamma m_{t-1} + \eta_t \nabla f(x_t - \gamma m_{t-1}))$$


改进了**SGD-M**，使之更精确；。

## AdaGrad

$$x_{t+1} = x_t - \eta_t \nabla f(x_t)$$

其中$\eta_t=\eta/\sqrt{n_t+\delta}$，$n_t=\sum_{i=1}^t f(x_i).*f(x_i)$

优点：

* 学习率随时间逐渐降低。
* 对更新频繁的学习率较低，更新缓慢的学习率高，能约束震荡，适合稀疏梯度。

缺点：

* 难以估计初始梯度大小，导致参数$\eta$十分敏感。
* 叠加所有时间的梯度可能导致，初始误差的累积。
* 学习率趋于0时可能提前结束训练。

## AdaDelta

令
$$E[g.^2]_t=\rho * E[g^2]_{t-1} + (1-\rho) * g^2_t$$
则
$$x_{t+1}=x_t-$$

