---
title: 微分方程与高中物理问题
date: 2025-08-20 10:58:22
tags:
  - 物理
  - 数学
categories:
- study
- physics
- maths
toc: true
abbrlink: 194655
---

最近学习了微分方程，那么就试着拿他来解决一些问题吧。

## 模型一：阻力与速度成正比的平抛运动

### 来源

<img src="194655/2.jpg" style="width:50%;" alt="题目"/>

{% note info %}
这道题可以使用配速法求解，但是这样的方法需要一定的思维量，没有这么简单直接。
{% gi 3 3 %}
![程力](194655/a.png)
![程力](194655/b.png)
![程力](194655/c.png)
{% endgi %}
{% endnote %}

---

### 计算

**Q**：一个质量为$m$的小球自$A$点以水平速度$v_{0}$抛出，在重力和空气阻力作用下，近一段时间后落在$B$点。小球在空中所受的空气阻力满足
$$\mathbf{f} =-k\mathbf{v} $$
其中$k$为正的常量，$v$为小球在运动中的速度，试求水平与竖直方向上位移、速度、加速度的表达式。
<img src="194655/1.png" style="width:50%;" alt="模型一"/>

**A**：
首先将速度与阻力进行正交分解，阻力正交分解后可以得到<img align="right" src="194655/3.png" style="width:40%;margin-left: 20px;" alt=""/>
$$fcos\theta=kvcos\theta=kv_{x}$$
同理得到$fsin\theta=kv_{v}$
列出牛顿第二定律
$$ma_{x}=-kv_{x}$$
$$ma_{y}=kv_{y}-mg$$
解这两个微分方程，前一个可以直接解出：
$$v_{x}=e^{-\frac{k}{m}t}$$
后一个我们将其改写为
$$\frac{\mathrm{d} v_{y}}{\mathrm{d} t} =\frac{k}{m} v_{y}-g$$
$$\frac{\mathrm{d} v_{y}}{\frac{k}{m} v_{y}-g} = \mathrm{d} t$$
求积分
$$\int \frac{\mathrm{d} v_{y}}{\frac{k}{m} v_{y}-g} = \int \mathrm{d} t$$
换元，设$u=\frac{k}{m}v_{y}-g$，有$dt=\frac{m}{k}du$，积分化为
$$\int \frac{1}{u} \frac{m}{k}\mathrm{d}u = \int \mathrm{d} t$$
得
$$\frac{m}{k}ln(g-\frac{k}{m}v_{y} )+C=t $$
当$t=0$，$v_{y}=0$，解出
$$C=-\frac{m}{k}ln(g) $$
得
$$\frac{k}{m}t=ln(\frac{k}{mg}v_{y}-1 ) $$
最后解得
$$v_{y}=\frac{mg}{k}(1-e^{-\frac{k}{m}t }) $$
