# <p align=center>`Neural Radiance Fields`</p>

> 我们总希望机器能做到人能做到的事情，甚至要比人做得更好。



## Content

- Improve Performance
  - [NeRF++](#NeRF++)
  - [UNISURF](#UNISURF)

---

<span id="UNISURF"></span>
[UNISURF: Unifying Neural Implicit Surfaces and Radiance Fields for Multi-View Reconstruction](https://arxiv.org/pdf/2104.10078.pdf)  
**[`arxiv`] (`MPI`)**  
*Michael Oechsle, Songyou Peng, Andreas Geiger*

<details><summary>Click to expand</summary>

<div align="center"><img width="500" src="https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20210428214156.png" ></div>

> **Summary**

Combine **volumetric radiance** (powerful for "unsupervised" coarse scene) and **surface rendering** (accurate reconstruction).

> **Details**


$$
\begin{aligned}
\mathcal{L} &=\mathcal{L}_{r e c}+\lambda \mathcal{L}_{r e g}
\\
\mathcal{L}_{r e c} &=\sum_{\mathbf{r} \in \mathcal{R}}\left\|\hat{C}_{v}(\mathbf{r})-C(\mathbf{r})\right\|_{1} \\
\mathcal{L}_{r e g} &=\sum_{\mathbf{x}_{s} \in \mathcal{S}}\left\|\mathbf{n}\left(\mathbf{x}_{s}\right)-\mathbf{n}\left(\mathbf{x}_{s}+\boldsymbol{\epsilon}\right)\right\|_{2}
\\
\mathbf{n}\left(\mathbf{x}_{s}\right)&=\frac{\nabla_{\mathbf{x}_{s}} o_{\theta}\left(\mathbf{x}_{s}\right)}{\left\|\nabla_{\mathbf{x}_{s}} o_{\theta}\left(\mathbf{x}_{s}\right)\right\|_{2}}
\end{aligned}
$$
将 surface rendering 和 volume rendering 写成
$$
\begin{aligned}
&\hat{C}_{v}(\mathbf{r})=\sum_{i=1}^{N} o_{\theta}\left(\mathbf{x}_{i}\right) \prod_{j<i}\left(1-o_{\theta}\left(\mathbf{x}_{j}\right)\right) c_{\theta}\left(\mathbf{x}_{i}, \mathbf{n}_{i}, \mathbf{h}_{i}, \mathbf{d}\right) \\
&\hat{C}_{s}(\mathbf{r})=c_{\theta}\left(\mathbf{x}_{s}, \mathbf{n}_{s}, \mathbf{h}_{s}, \mathbf{d}\right)
\end{aligned}
$$

</details>

---

<span id="NeRF++"></span>
[NeRF++: Analyzing and Improving Neural Radiance Fields](https://arxiv.org/pdf/2010.07492.pdf)  
**[`Arxiv 2020`] (`Cornell Tech, iNTEL`)**  
*Kai Zhang, Gernot Riegler, Noah Snavely, Vladlen Koltun*

<details><summary>Click to expand</summary>

<div align=center><img width="700" src="https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20210908171414.png"/></div>

> **Summary**

- resolve shape-radiance ambiguity (incorrect geometry bring correct rendering images because the radiance fields are degenerate), 想象不规则的体退化成一个球面，表面的颜色能够渲染出对应的图像，在一定范围内是可以过拟合学到的。**本质是缺少约束带来的过拟合问题**。
- remedy parameterization of unbounded scenes in the case of 360° captures.

> **Details**

- As $\sigma$ deviates from the correct shape, c must in general become a high-frequency function with respect to d to reconstruct the input images. For the correct shape, the surface light field will generally be much smoother (in fact, constant for Lambertian materials). **The higher complexity required for incorrect shapes is more difficult to represent with a limited capacity MLP.**



如何来实验验证，是重点，可以学习一下是怎么开展的。

</details>

---

