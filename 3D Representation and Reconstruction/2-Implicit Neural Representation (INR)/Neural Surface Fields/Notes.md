# <p align=center>`Neural Implicit Surfaces`</p>



## Introduction

一个使用SDF，一个使用occupancy network，然后对应不同的损失和正则loss

zero level-set



学出很多等高面，然后0登高面就是表面

有关 Level set equation 的解释，$\phi(x(t), t) = 0$

https://profs.etsmtl.ca/hlombaert/levelset/



![image-20210219111025930](https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20210219111027.png)

Humans possess an impressive intuition for 3D shapes: given partial observations of an object we can easily imagine the shape of the complete object. Now we want to reproduce this ability with algorithms.



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





---


<span id="DeepSDF"></span>
[DeepSDF: Learning Continuous Signed Distance Functions for Shape Representation](https://arxiv.org/abs/1901.05103)  
**[`CVPR 2019`] [`UW, MIT,Facebook`]**  
*Jeong Joon Park, Peter Florence, Julian Straub, Richard Newcombe, Steven Lovegrove*

<details><summary>Click to expand</summary><p>


<img src="https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20210225212510.png" alt="image-20210225212508695" style="zoom:50%;" />

> **Summary**

In this work, we introduce DeepSDF, a learned continuous Signed Distance Function (SDF) representation of a class of shapes that enables high quality shape representation, interpolation and completion from
partial and noisy 3D input data.

> **Details**

(from [DIT]())

It defines a surface as the level set of a signed distance field (SDF), e.g. $\mathcal{F}(\boldsymbol{p})=0$, where $\boldsymbol{p} \in \mathbb{R}^3$ donates a 3D point and $\mathcal{F}: \mathbb{R}^3 \mapsto \mathbb{R}$ is a function approximated using a deep neural network.

In practice, in order to represent multiple object instances using one neural network, the function $\mathcal{F}$ also takes a condition variable $\boldsymbol{c}$ as input and thus can be written as:
$$
\mathcal{F}(\boldsymbol{p}, \boldsymbol{c})=s: \boldsymbol{p} \in \mathbb{R}^{3}, \boldsymbol{c} \in \mathcal{X}, s \in \mathbb{R}
$$
The object surface can be extracted using [Marching Cube]().



$\boldsymbol{c}$ is a high-dimensional latent code and each shape instance has a unique code. All latent codes are firstly initialized with Gaussian noise and then optimized in parallel with network training.



**Learning the latent space of shapes.** Training a specific neural network for each shape is neither feasible nor very useful. Instead, we want a model that can represent a wide variety of shapes, discover their common properties, and embed them in a low dimensional latent space.

**Auto-decoder-based Training.** 

a dataset of $N$ shapes, each shape of $K$ point samples. 
$$
X_{i}=\left\{\left(\boldsymbol{x}_{j}, s_{j}\right): s_{j}=S D F^{i}\left(\boldsymbol{x}_{j}\right)\right\}, ~~~~i = 1, 2 ,\dots, N
$$
each shape is also paired with a latent code $\boldsymbol{z}_i$. In the latent shape-code space, we assume the prior distribution $p(\boldsymbol{z}_i)$ to be a zero-mean multivariate-Gaussian with a spherical covariance $\sigma^2I$.

hope the latent code space is a compact manifold in order to help converge to good solutions.



The SDF prediction $\tilde{s}_{j}=f_{\theta}\left(\boldsymbol{z}_{i}, \boldsymbol{x}_{j}\right)$ and the loss function $\mathcal{L}\left(\tilde{s}_{j}, s_{j}\right)$.

</p></details>

---

<span id="MetaSDF"></span>
[MetaSDF: Meta-learning Signed Distance Functions](https://arxiv.org/pdf/2006.09662.pdf)  
**[`NeurIPS 2020`] (`Stanford`)**  
*Vincent Sitzmann, Eric R. Chan, Richard Tucker, Noah Snavely, Gordon Wetzstein]*

a dataset $\mathcal{D}$ of $N$ shapes, each shape is represented by a set of points $X_i$ consisting of $K$ point samples


$$
\mathcal{D} = \{X_i\}_{i=1}^N, \qquad X_i = \{(\mathbf{x}_j, s_j):s_j = SDF_i(\mathbf{x}_j)\}_{j=1}^K
$$
where $\mathbf{x}_j$ are spatial coordinates, and $s_j$ are the signed distances at these spatial coordinates





A point set generation network for 3d object reconstruction from a single image
