# <p align=center>`Neural Implicit Surfaces`</p>



## Introduction

一个使用SDF，一个使用occupancy network，然后对应不同的损失和正则loss





[NeuS](#NeuS)

[VolSDF](#VolSDF)

---

<span id="NeuS"></span>
[NeuS: Learning Neural Implicit Surfaces by Volume Rendering for Multi-view Reconstruction](https://arxiv.org/pdf/2106.10689.pdf)  
**[`NeurIPS 2021`]  (`HKU, MIT`)**   
*Peng Wang, Lingjie Liu, Yuan Liu, Christian Theobalt, Taku Komura, Wenping Wang*

<details><summary>Click to expand</summary>

<div align=center><img width="700" src="https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20210916164746.png"/></div>

> **Summary**

A method to reconstruct surface with high fidelity from 2D images. NeuS uses the SDF for surface representation and uses a novel volume rendering scheme to learn. **Only focus on solid objects.**

they replace the local transparency function with an occupancy network

> **Details**

Solve the problems:

- simply applying a standard volume rendering method to the density associated with SDF would lead to discernible bias. :arrow_right: propose a novel volume rendering scheme to ensure unbiased surface reconstruction in the first-order approximation of SDF.



NeuS consists of two networks:

- $f: \mathbb{R}^3 \rightarrow \mathbb{R}$ spatial point :arrow_right: its signed distance
- $c: \mathbb{R}^3 \times \mathbb{S}^2 \rightarrow \mathbb{R}^3$ spatial point and view direction :arrow_right: color

$$
\mathcal{S} = \{\mathbf{x} \in \mathbb{R}^3 \mid f(\mathbf{x}) = 0 \}
$$

logistic density distribution $\phi_{s}(x)=s e^{-s x} /\left(1+e^{-s x}\right)^{2}$, which is the derivative of the Sigmoid function $\Phi_s(x) = (1 + e^{-sx})^{-1}$. Using S-density field $\phi_s(f(x))$ to render.

</details>

---

<span id="VolSDF"></span>
[Volume Rendering of Neural Implicit Surfaces](https://arxiv.org/pdf/2106.12052.pdf)  
**[`Arxiv 2021`] (`Weizmann Institute of Science, Facebook`)**  
*Lior Yariv, Jiatao Gu, Yoni Kasten, Yaron Lipman*

<details><summary>Click to expand</summary>

<div align=center><img width="700" src="https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20210916202925.png"/></div>

> **Summary**

They model the volume density ($\sigma$) as a function of the geometry rather than model the geometry as a function of the volume density.
$$
\sigma = f(geometry)  \Rightarrow  geometry = f(\sigma)
$$
The geometry is represented by a signed distance function (SDF).

They represent the desity as a funtion of the signed distance to the scene’s surface.

> **Details**

Their model is:
$$
\sigma(\boldsymbol{x})=\alpha \Psi_{\beta}\left(-d_{\Omega}(\boldsymbol{x})\right)
$$
where $\Omega \subset \mathbb{R}^{3}$  is the space occupied by object, and $\mathcal{M}=\partial \Omega$ is its boundary surface, and $\alpha, \beta$ are learnable para.
$$
\text{Indicator Function: } \mathbf{1}_{\Omega}(\boldsymbol{x})= \begin{cases}1 & \text { if } \boldsymbol{x} \in \Omega \\ 0 & \text { if } \boldsymbol{x} \notin \Omega\end{cases}
\\
\text{SDF: } d_{\Omega}(\boldsymbol{x})=(-1)^{1_{\Omega}(\boldsymbol{x})} \min _{\boldsymbol{y} \in \mathcal{M}}\|\boldsymbol{x}-\boldsymbol{y}\|_{2}
\\
\text{Cumulative Distribution Function (CDF): } \Psi_{\beta}(s)= \begin{cases}\frac{1}{2} \exp \left(\frac{s}{\beta}\right) & \text { if } s \leq 0 \\ 1-\frac{1}{2} \exp \left(-\frac{s}{\beta}\right) & \text { if } s>0\end{cases}
$$
They also do a disentanglement of geometry and appearance:





</details>

---



[Neural Splines: Fitting 3D Surfaces with Infinitely-Wide Neural Networks](https://arxiv.org/pdf/2006.13782.pdf)  
**[`CVPR 2021`] (`NYU, Amazon`)**  
*Francis Williams, Matthew Trager, Joan Bruna, Denis Zorin*



> **Problem Formulation**

$$
\min_\theta L(\theta)=\frac{1}{2} \sum_{j=1}^{s}\left|f\left(x_{j} ; \theta\right)-y_{j}\right|^{2}+\left\|\nabla_{x} f\left(x_{j} ; \theta\right)-n_{j}\right\|^{2}
$$

