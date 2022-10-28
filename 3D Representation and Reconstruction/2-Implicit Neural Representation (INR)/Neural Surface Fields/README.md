# <p align=center>`Neural Surface Fields`</p>

A collection of resources on Neural Implicit Surfaces. The goal is to reconstruct surfaces from a sparse set of multi-view images. And then we can synthesize novel views of a scene.

## Introduction

This line of research focuses on representing the scene’s geometry implicitly using a neural network, making the surface rendering process differentiable. 



Previous works of neural volume rendering techniques which is modeled using a generic density function, 



The **geometry** is represented by the object surface.



In this research field, the main stream techniques represent both the density and light fields as neural networks lead to excellent prediction of novel views by learning only from a sparse set of input images. In more detail, Nerf, Nerv, Nerd approximate the integral as alpha-composition in a differentiable way, allowing to learn simultaneously both from input images.



> Chinese Description: 一个高保真的3D重建，应该保证物体表面是足够真实的，过去基于体密度的方法，是通过找体密度的一个等势面来确定表面的（这种方面会带来噪声，和低保真度）。因此更好的一种方式是



Because of the lack of sufficient surface constraints in the representation.



The main drawback of these methods is their requirement of **masks that separate objects from the background.** require foreground mask as supervision

struggle with severe self-occlusion or thin structures

Learning to render surfaces directly tends to grow extraneous parts due to optimization problems.



体渲染的好处，



Choose implicit functions with MLPs due to its expressive representation power and low memory foot-print.



non-Lambertian surfaces and thin structures



These methods can be divided into two categories:

- ...



- SDF or occupancy




making the surface rendering process differentiable

requirement of masks that separate objects from the background.





如果仅仅是重建表面，光线和表面就一个交点， single intersection point for each ray  这样的话梯度也只存在于这一点









### Problem Formulation

> Surface Reconstruction

a set of posed images $\{\mathcal{I}_k\}$ of a 3D object, goal is to reconstruct the surface $\mathcal{S}$ of the object.



We want to find a scalar function $f: \mathbb{R}^3 \rightarrow \mathbb{R}$ 

Zero level set $S = \{p: f(p) = 0 \} \sub \mathbb{R}^3$ is the estimated surface.







## Literature

> Click the [title]() will jump to the Arxiv-pdf link | click the Notes will jump to the personal note.



#### + Masks (difficult to optimize)

- <span id="DVR"></span>
  [Differentiable Volumetric Rendering: Learning Implicit 3D Representations without 3D Supervision](https://arxiv.org/pdf/1912.07372.pdf)  
  *Michael Niemeyer, Lars Mescheder, Michael Oechsle, Andreas Geiger*  
  **[`CVPR 2020`] (`MPI`)** [[Code](https://github.com/autonomousvision/differentiable_volumetric_rendering)]  

- <span id="IDR"></span>
  [Multiview Neural Surface Reconstruction by Disentangling Geometry and Appearance](https://arxiv.org/pdf/2003.09852.pdf)  
  *Lior Yariv, Yoni Kasten, Dror Moran, Meirav Galun, Matan Atzmon, Ronen Basri, Yaron Lipman*  
  **[`NeurIPS 2020`] (`Weizmann Institute of Science`)**

- <span id="NLR"></span>
  [Neural Lumigraph Rendering](https://arxiv.org/pdf/2103.11571.pdf)  
  *Petr Kellnhofer, Lars Jebe, Andrew Jones, Ryan Spicer, Kari Pulli, Gordon Wetzstein*  
  **[`CVPR 2021`] (`Raxium, Stanford`)**



#### + Volume Rendering

- <span id="VolSDF"></span>
  [Volume Rendering of Neural Implicit Surfaces](https://arxiv.org/pdf/2106.12052.pdf)  
  *Lior Yariv, Jiatao Gu, Yoni Kasten, Yaron Lipman*  
  **[`NeurIPS 2021`] (`Weizmann Institute of Science, Facebook`)**  

- <span id="Neural-Splines"></span>
  [Neural Splines: Fitting 3D Surfaces with Infinitely-Wide Neural Networks](https://arxiv.org/pdf/2006.13782.pdf)  
  *Francis Williams, Matthew Trager, Joan Bruna, Denis Zorin*  
  **[`CVPR 2021`] (`NYU, Amazon`)**  

- <span id="UNISURF"></span>
  [UNISURF: Unifying Neural Implicit Surfaces and Radiance Fields for Multi-View Reconstruction](https://arxiv.org/pdf/2104.10078.pdf)  
  *Michael Oechsle, Songyou Peng, Andreas Geiger*  
  **[`ICCV 2021`] (`MPI`)**  

- <span id="NeuS"></span>
  [NeuS: Learning Neural Implicit Surfaces by Volume Rendering for Multi-view Reconstruction](https://arxiv.org/pdf/2106.10689.pdf)  
  *Peng Wang, Lingjie Liu, Yuan Liu, Christian Theobalt, Taku Komura, Wenping Wang*  
  **[`NeurIPS 2021`]  (`HKU, MIT`)**   



<i>If warmup is the answer, what is the question?</i>

<p style="color:blue;">Blue text</p>

