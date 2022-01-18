# <p align=center>`Learn 3D object from 2D images` </p>

A collection of resources on learning 3D object from 2D images.







[toc]

## Introduction

alias: image-based 3D reconstruction



significant advances have been made towards complete geometric reconstruction from an RGB image input.



given a set of photographs of an object or a scene, estimate the most likely 3D shape that explains those photographs, under the assumptions of known materials, viewpoints, and lighting conditions.

![image-20211121113331345](https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20211121113332.png)



existing methods:

- rely on explicit supervision



Feature: ambiguities



If the materials, viewpoints, and lighting are not known, this will be generally an ill-posed problem because combinations of geometry, materials, viewpoints, and lighting can produce exactly the same photographs (**ambiguity**). As a result, without further assumptions, no single algorithm can correctly reconstruct the 3D geometry from photographs alone.



GIven a photograph of a scene, one can infer the underlying geometric structures and identify object and structure semantics, even from a partial, single view observation.



Some methods consider 3D semantic reconstruction and instance reconstruction independently. 



### Problem Statement

Let $\mathbf{I} = \{I_k, k=1, \dots, n\}$ be a set of $n \ge 1$ RGB images of one or multiple objects $X$. 3D reconstruction can be summarized as the process of learning a predictor $f_\theta$ that can infer a shape $\hat{X}$ that is as close as possible to the unknown shape $X$.

The function $f_{\theta}$ is the minimizer of a reconstruction objective $\mathcal{L}(\mathbf{I}) = d(f_\theta (\mathbf{I}), X)$. Here, $d(\cdot)$ is a certain measure of distance between the target shape $X$ and the reconstructed shape $f(\mathbf{i})$.



### Methods

Multi-view Stereo (MVS) is the general term given to a group of techniques that use stereo correspondence as their main cue and use more than two images. **An MVS algorithm is only as good as the quality of the input images and camera parameters.** A generic MVS pipeline is；

- collect images,
- compute camera parameters for each image,
- reconstruct the 3D geometry of the scene from the set of images and corresponding camera parameters,
- optionally reconstruct the materials of the scene.



#### > compute the camera parameters

> Camera Models, ref to 

Structure from Motion (SfM)





predict depth

Revisiting single image depth estimation: Toward higher resolution maps with accurate object boundaries







## Literature

### Survey

Multi-View Stereo: A Tutorial  
*Yasutaka Furukawa, Carlos Hernández*  
**[`2015`]**

[Image-based 3D Object Reconstruction: State-of-the-Art and Trends in the Deep Learning Era](https://arxiv.org/pdf/1906.06543.pdf)  
*Xian-Feng Han, Hamid Laga, Mohammed Bennamoun*  
**[`TPAMI 2019`]**

### Category

<span id="DOVE"></span>
[DOVE: Learning Deformable 3D Objects by Watching Videos](https://arxiv.org/pdf/2107.10844.pdf)  
*Shangzhe Wu, Tomas Jakab, Christian Rupprecht, Andrea Vedaldi*  
**[`Arxiv 2021`]**



**learn from RGB**

[3D Scene Reconstruction with Multi-layer Depth and Epipolar Transformers]()  
*Daeyun Shin, Zhile Ren, Erik B. Sudderth, Charless C. Fowlkes*  
**[`ICCV 2019`] (`UCI, Georgia`)**

[CoReNet: Coherent 3D scene reconstruction from a single RGB image](https://arxiv.org/pdf/2004.12989.pdf)  
*Stefan Popov, Pablo Bauszat, Vittorio Ferrari*  
**[`ECCV 2020`] ()**

[3D Scene Reconstruction from a Single Viewport](https://www.ecva.net/papers/eccv_2020/papers_ECCV/papers/123670052.pdf)  
*Maximilian Denninger, Rudolph Triebel*  
**[`ECCV 2020`] (`DLR, TUM`)**

[Panoptic 3D Scene Reconstruction From a Single RGB Image](https://arxiv.org/pdf/2111.02444.pdf)  
*Manuel Dahnert, Ji Hou, Matthias Nießner, Angela Dai*  
**[`NeurIPS 2021`] (`TUM`)**



## Main Research Group

