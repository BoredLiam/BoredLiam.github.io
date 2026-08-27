---
title: 幂平均函数和不等式链
tags: 
  - math
categories:
  - study
abbrlink: 9191156
date: 2026-08-27 19:30:47
---

发现了一个有趣的函数，通过它可以方便地证明$n$阶不等式链。
当然这不算什么新鲜事，只是可以当作一个求导的小练习。

<!-- more -->

## 幂平均函数

我们定义幂平均函数$f(x)$为：
$$f(x)=(\frac{a^{x}+b^{x}}{2})^{\frac{1}{x}}$$
其中$(x\ne0,a>0,b>0,a\ne b)$

那么根据$f'(x)>0$可以得到
$$f(-1)\leq \lim_{x \to 0}f(x)\leq f(1)\leq f(2)\leq ... \leq f(n)$$
即
$$\frac{2}{\displaystyle{\frac{1}{a}+\frac{1}{b}}}\leq \sqrt{ab}\leq \frac{a+b}{2}\leq \sqrt{\frac{a^2 +b^2}{2}}\leq ...\leq \sqrt[n]{\frac{a^n +b^n}{2}}$$

## 证明1：$f(x)$单调递增

令
$$y=(\frac{a^{x}+b^{x}}{2})^{\frac{1}{x}}$$
则
$$lny=\frac{1}{x}\frac{a^{x}+b^{x}}{2}$$
两边同时对$x$求导得
$$\frac{1}{y}\frac{\mathrm{d}y}{\mathrm{d}x}=-\frac{1}{x^2}ln\frac{a^{x}+b^{x}}{2}+\frac{1}{x}·\frac{\mathrm{d}}{\mathrm{d}x}(ln\frac{a^{x}+b^{x}}{2})$$

> 其中，令$t=\displaystyle{\frac{a^{x}+b^{x}}{2}}$，则有
> $$\frac{\mathrm{d}}{\mathrm{d}x}(ln\frac{a^{x}+b^{x}}{2})=\frac{\mathrm{d}}{\mathrm{d}t}(lnt)·\frac{\mathrm{d}}{\mathrm{d}x}(\frac{a^{x}+b^{x}}{2})$$
> $$=\frac{1}{t}(\frac{1}{2}a^x lna+\frac{1}{2}b^x lnb)$$
> $$=\frac{a^x lna+b^x lnb}{a^x+b^x}$$

计算代入得
$$\frac{1}{y}\frac{\mathrm{d}y}{\mathrm{d}x}=-\frac{1}{x^2}ln\frac{a^{x}+b^{x}}{2}+\frac{1}{x}\frac{a^x lna+b^x lnb}{a^x+b^x}$$
将$y$乘过去，并提取公因式
$$\frac{\mathrm{d}y}{\mathrm{d}x}=(\frac{a^{x}+b^{x}}{2})^{\frac{1}{x}}\frac{1}{x^2}(\frac{a^x lna+b^x lnb}{a^x+b^x}x-ln\frac{a^{x}+b^{x}}{2})$$
接下来提取出一个$\displaystyle{\frac{2}{a^{x}+b^{x}}}$放在括号外面，顺便把一个$x$放进对数里
$$\frac{\mathrm{d}y}{\mathrm{d}x}=(\frac{a^{x}+b^{x}}{2})^{\frac{1}{x}}\frac{1}{x^2}\frac{2}{a^{x}+b^{x}}(\frac{a^x lna^{x}+b^x lnb^{x}}{2}-\frac{a^{x}+b^{x}}{2}ln\frac{a^{x}+b^{x}}{2})$$
为什么这么做呢？别忘了我们是要证明导数大于$0$，此时分离出的前半部分显然有
$$(\frac{a^{x}+b^{x}}{2})^{\frac{1}{x}}\frac{1}{x^2}\frac{2}{a^{x}+b^{x}}>0$$
所以我们只需证明
$$\frac{a^x lna^{x}+b^x lnb^{x}}{2}>\frac{a^{x}+b^{x}}{2}ln\frac{a^{x}+b^{x}}{2}$$
即可

我们观察这个构造出的形式，可以发现只要令$g(t)=tlnt$ $(t>0)$
因为
$$g'(t)=lnt+1$$
$$g''(t)=\frac{1}{t}>0$$
说明$g(t)$为上凸函数

那么
$$\frac{g(a^x)+g(b^x)}{2}>g(\frac{a^{x}+b^{x}}{2})$$
即
$$\frac{a^x lna^{x}+b^x lnb^{x}}{2}>\frac{a^{x}+b^{x}}{2}ln\frac{a^{x}+b^{x}}{2}$$
那么便证明了$\displaystyle{\frac{\mathrm{d}y}{\mathrm{d}x}}>0$

## 证明2：$0$处的极限

我们来证明
$$\lim_{x \to 0} f(x)=\sqrt{ab}$$

其实就是简单的洛必达
$$\lim_{x \to 0}(\frac{a^{x}+b^{x}}{2})^{\frac{1}{x}}=e^{\lim\limits_{x\to 0}\frac{1}{x}ln\frac{a^{x}+b^{x}}{2}}$$
而其中
$$\lim_{x\to 0}\frac{1}{x}ln\frac{a^{x}+b^{x}}{2}=\lim_{x\to 0}\frac{ln\frac{a^{x}+b^{x}}{2}}{x}\overset{\text{洛必达}}{=}\lim_{x\to 0}\frac{a^x lna+b^x lnb}{a^x+b^x}=\frac{lna+lnb}{2}$$
代入得
$$\lim_{x \to 0}(\frac{a^{x}+b^{x}}{2})^{\frac{1}{x}}=e^{\frac{lna+lnb}{2}}=\sqrt{ab}$$
由此得证

## 后记

顺便一提：这个[知乎文章：LaTeX中如何让行内分式调整为正常大小？](https://zhuanlan.zhihu.com/p/432757682)里的方法还挺有用的
公式也贴在这里吧

```latex
\displaystyle{\frac{n}{2}} %  将\frac{n}{2}的行内公式尺寸强制调整为行间公式尺寸，
```
