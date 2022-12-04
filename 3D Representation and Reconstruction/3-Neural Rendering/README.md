[toc]

# Neural Rendering Notes

Related repositories:

- [collection of neural rendering papers](https://github.com/weihaox/awesome-neural-rendering) by 

- [collection of neural radiance fields papers](https://github.com/yenchenlin/awesome-NeRF) by 



## Table of Contents





## Introduction

> neural rendering 包含了 NeRF，指的是用 神经表征和渲染 的一类方法，它是一类方法或者技术的总称。
>
> The goal of neural rendering is to project a 3D neural scene representation into one or multiple 2D images.
>
> 简单说neural rendering可以涵盖所有新的带neural的技术



Traditional 2D GANs take in a latent vector $$\mathbf{z} \sim p_{\mathbf{z}}$$ and directly produce a 2D image.

Now, instead of directly generating an image from the input noise $$\mathbf{z}$$, new generator $$G(\mathbf{z}, \xi)$$ produces an implicit 3D radiance field conditioned on $\mathbf{z}$. Then novel view image is rendered from this radiance field by volume rendering.



Computer graphics + generative model two areas come together -> neural rendering 



The first publication that used the term "neural rendering" is *Generative Query Network* (GQN). A newest state-of-the-art report formally defines *Neural Rendering* as:

> Deep image or video generation approaches that enable explicit or implicit control of scene properties such as illumination, camera parameters, pose, geometry, appearance, and semantic structure.

**Neural volume rendering** refers to methods that generate <u>images</u> or <u>video</u> by tracing a ray into the scene and taking an integral of some sort over the length of the ray. Typically a neural network like a multi-layer perceptron (MLP) encodes a function from the 3D coordinates on the ray to quantities like density and color, which are integrated to yield an image.

## Challenge/Direction

**3D Representation**

- methods

我们既可以用一段code来表征，也可以用神经网络的一组权重来表征

从2D表征引入，有什么意义呢---压缩大小，提取特征，

很自然的迁移到3D表征

**Representation Template**

这是为了提高表征效率的一个方法，也是非常自然的，

带来的好处有，速度更快，只需要在模板上进行修改 （想想身边所有模板的好处）

**Style Transfer**

类比于image的style transfer，舶来主义

**Rendering**

这不是我们研究的重点，拿来直接用，主要就是光影的问题

这里面又还有分支

**Relight**

---



You need to know first

- [ ] Physical Image Formation

  light source, scene geometry, material properties, light transport, optics, sensor behavior

- [ ] 



2D-to-3D representation



3D-to-3D image rendering

 

3D-aware image synthesis

voxel-based representation



A coordinate-based MLP model. 

<img src="https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20210123193611.png" alt="image-20210123193611687" style="zoom:50%;" />

the issue is: computing the network weights $\theta$ is very expensive, especially recover a high resolution radiance field as in NeRF.

Approaches includes:

- concatenating a latent vector to the input coordinate and supervising a single neural network to represent an entire class of signals [Occupancy networks]() [DeepSDF]()
- training a hypernetwork to map from signal observations (or a latent code) to MLP weights

Implicit neural representations with periodic activation functions

Scene representation networks

MetaSDF



Task field:

- relight

[NeRV](# NeRV)

Deep reflectance volumes

A neural rendering framework for free-viewpoint relighting

Deferred neural lighting

Single-shot neural relighting and SVBRDF estimation

Neural light transport for relighting and view synthesis



**visual quality** 

> low-resolution output, overly smoothed, discontinuous surfaces, topological noise and irregularities



## Shape Generation

Learning Implicit Fields for Generative Shape Modeling

> implicit field decoder









## Research Teams

[Berkeley Artificial Intelligence Research Lab (BAIR)](https://bair.berkeley.edu/)

- AP. [Ren Ng](https://www2.eecs.berkeley.edu/Faculty/Homepages/yirenng.html)
- AP. [Angjoo Kanazawa](https://people.eecs.berkeley.edu/~kanazawa/)
- PhD. [Ben Mildenhall](https://people.eecs.berkeley.edu/~bmild/)
- PhD. [Matthew Tancik](https://www.matthewtancik.com/)

Selected works: `NeRF` | `pixelNeRF`



[Max Planck Institute Graphics Vision & Video Group](http://gvv.mpi-inf.mpg.de/GVV_Team.html) 

- Prof. [Christian Theobalt](https://people.mpi-inf.mpg.de/~theobalt/)
- Prof. [Andreas Geiger](http://www.cvlibs.net/)
- PhD. [Ayush Tewari](https://people.mpi-inf.mpg.de/~atewari/)
- Ph.D. [Michael Niemeyer](https://m-niemeyer.github.io/)

Selected works: `PatchNets` |



[Stanford Computational Image Lab](http://www.computationalimaging.org/team/)

- AP. [Gordon Wetzstein](http://web.stanford.edu/~gordonwz/)
- Postdoc. [Vincent Sitzmann](https://vsitzmann.github.io/)

Selected works: `SRN` | `MetaSDF`



[University of Washington Graphics and Imaging Laboratory](https://grail.cs.washington.edu/)

- Prof. [Steven Seitz](https://homes.cs.washington.edu/~seitz/)
- PhD. [Keunhong Park](https://keunhong.com/)
- PhD. [Jeong Joon Park](https://jjparkcv.github.io/)

Selected works: `Nerfies` | `DeepSDF`

























## Literature

### survey

[State of the Art on Neural Rendering](https://arxiv.org/pdf/2004.03805.pdf)  
**[`EUROGRAPHICS 2020`]**

[Advances in Neural Rendering](https://arxiv.org/pdf/2111.05849.pdf)  
**[`arxiv 2021`]**





<span id="GQN"></span>
[Neural scene representation and rendering](https://science.sciencemag.org/content/360/6394/1204/tab-pdf)  
*Tero Karras, Samuli Laine, Timo Aila*  
**[`Science 2018`] (`DeepMind `)** [[Code](https://github.com/NVlabs/stylegan)]  

<details><summary>Click to expand</summary><p>


> **Summary**

It enables machines to learn to perceive their surroundings based on a representation and generation network. The authors argue that the network has an implicit notion of 3D due to the fact that it could take a varying number of images of the scene as input, and output arbitrary views with correct occlusion.

</p></details>

---



# Rendering



这里关心的是神经渲染这一类，因为要和神经表征去搭配。主要的方法是 rasterization and raytracing

- volume rendering

  integrate densities by drawing samples along the viewing rays

- surface rendering

  Differentiable volumetric rendering (DVR)

  Multiview neural surface reconstruction (IDR)

  

## Non-differentiable Rendering

a discrete operation called rasterization





## Differentiable Rendering

a fundamental tool in computer graphics that convert 3D models into 2D images.



neural networks bring "neural rendering" because natural differentiable





---

Neural 3d mesh renderer

CVPR 2018

Differentiable Monte Carlo Ray Tracing through Edge Sampling

SIGGRAPH 2018

[Soft Rasterizer: A Differentiable Renderer for Image-based 3D Reasoning](https://arxiv.org/pdf/1904.01786.pdf)  
Shichen Liu, Tianye Li, Weikai Chen, Hao Li  
[ICCV 2019] ()



Opendr: An approximate differentiable renderer

ECCV 2014





Neural scene representation and rendering.

Science

[RenderNet: A deep convolutional network for differentiable rendering from 3D shapes](https://arxiv.org/pdf/1806.06575.pdf)  
Thu Nguyen-Phuoc, Chuan Li, Stephen Balaban, Yong-Liang Yang  
[NIPS 2018]



[Face-to-Parameter Translation for Game Character Auto-Creation](https://arxiv.org/pdf/1909.01064.pdf)  
*Tianyang Shi, Yi Yuan, Changjie Fan, Zhengxia Zou, Zhenwei Shi, Yong Liu*  
[ICCV 2019]







Dist: Rendering deep implicit signed distance function with differentiable sphere tracing

iterative ray marching to render a DeepSDF decoder

stratified random sampling 





## Volume Rendering

a set of $\mathcal{S}$ of sampled points per ray

A ray $x$ emanating from a camera position c in direction v 

x = c + tv 

volume rendering is approximating the integrated light radiance along this ray reaching the camera.




$$
\text{transparency: } T(t)=\exp \left(-\int_{0}^{t} \sigma(\boldsymbol{x}(s)) d s\right)
\\
\text{opacity: } O(t)=1-T(t)
\\
\text{PDF: } \tau(t)=\frac{d O}{d t}(t)=\sigma(\boldsymbol{x}(t)) T(t)
$$
the volume rendering is the expected light along the ray
$$
I(\boldsymbol{c}, \boldsymbol{v})=\int_{0}^{\infty} L(\boldsymbol{x}(t), \boldsymbol{n}(t), \boldsymbol{v}) \tau(t) d t
$$



can handle abrupt depth changes 

multiple points along the ray will effect the reconstruction, the gradient signals is full of the space rather than the thin surface.




## Surface Rendering







### Marching Cubes

- [Deep marching cubes: Learning explicit surface representations](http://www.cvlibs.net/publications/Liao2018CVPR.pdf)  
  **[`CVPR 2018`] (MPI, Zhejiang U)**  
  *Yiyi Liao, Simon Donné, Andreas Geiger*

- [Marching cubes: A high resolution 3D surface construction algorithm](https://people.eecs.berkeley.edu/~jrs/meshpapers/LorensenCline.pdf)  
  **[`SIGGRAPH 1987`] (`General Electric Company`)**  
  *William E. Lorensen, Harvey E. Cline*

