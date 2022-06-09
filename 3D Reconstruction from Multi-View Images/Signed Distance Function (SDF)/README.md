# signed distance functions (SDFs)

> 



zero level-set



学出很多等高面，然后0登高面就是表面





![image-20210219111025930](https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20210219111027.png)

Humans possess an impressive intuition for 3D shapes: given partial observations of an object we can easily imagine the shape of the complete object. Now we want to reproduce this ability with algorithms.



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