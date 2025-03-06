---
layout: post
title:  "DNN Optimization"
date:   2022-05-15 17:11:00 +0800
categories: DNN
---

# 优化方法

本文使用$\theta$表示神经网络中的可训练参数，使用$J(\theta)$表示给定网络参数下，训练集上的损失函数值，因此。由于找不到一个通用的方法直接求出损失函数的最小值，因此目前的优化过程基本上是根据梯度下降的过程。由于神经网络中参数很多，采用二阶方法需要很大的计算量，得不偿失，故通常使用一阶的优化算法。为了加快计算速度，一般都是使用小批量下降的过程，即每次算完该小批量所有样本的损失后再更新参数。

## GD (Gradient Descent)

$$\theta_{t+1} = \theta_t - \eta \nabla_{\theta}J(\theta_t)$$

_优点：_

* 一阶近似方法，计算量小。
* 适用范围广。

_缺点：_

* 容易陷入鞍点或局部最优点。
* 靠近输入层的梯度越来越不稳定可能导致梯度消失或者梯度爆炸。

## SGD (Stochastic Gradient Descent)

$$\theta_{t+1} = \theta_t - \eta_t g_t$$

且$E[g_t]=\nabla J(\theta_t)$

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

$$\theta_{t+1} = \theta_t - (\gamma m_{t-1} + \eta_t g_t)$$

且$E[g_t]=\nabla J(\theta_t)$

引入了动量的概念，有效地减少了震荡。

**NAG (Nesterov Accelerated Gradient)**

$$\theta_{t+1} = \theta_t - (\gamma m_{t-1} + \eta_t \nabla J(\theta_t - \gamma m_{t-1}))$$


改进了**SGD-M**，使之更精确；。

## AdaGrad

$$\theta_{t+1} = \theta_t - \eta_t \nabla J(\theta_t)$$

其中$\eta_t=\eta/\sqrt{n_t+\delta}$，$n_t=\sum_{i=1}^t J(\theta_i)*J(\theta_i)$

优点：

* 学习率随时间逐渐降低。
* 对更新频繁的学习率较低，更新缓慢的学习率高，能约束震荡，适合稀疏梯度。

缺点：

* 难以估计初始梯度大小，导致参数$\eta$十分敏感。
* 叠加所有时间的梯度可能导致，初始误差的累积。
* 学习率将逐渐趋于0，可能提前结束训练，特别是初始梯度较大的情况。

## AdaDelta

对**AdaGrad**可以进行一部分改进，

和**SGD**一样，$E[g_t]=\nabla J(\theta_t)$ 和**AdaGrad**一样，有

$$\theta_{t+1} = \theta_t - \eta_t \nabla J(\theta_t)$$

令

$$E[g^2]_t = \rho \cdot E[g^2]_{t-1} + (1-\rho) \cdot g^2_t$$

其中，$\rho$是学习衰减率，非常接近于1，学习率的计算如下：

$$\eta_t = \frac{\sqrt{\sum \Delta \theta^2_{t-1} + \delta}}{\sqrt{E[g^2]_t+\delta}}$$

优点：

* 解决了AdaGrad方法中学习率的一些问题，学习率无需手动设置，并且根据参数的更新历史自动调整学习率，也减少了学习率降低过快的问题，特别适用于处理稀疏数据。

缺点：

* 算法仍然对超参数$\rho$和$\delta$的选择非常敏感。
* 当初始化较差或者复杂问题时，收敛速度可能比其它算法更慢。
