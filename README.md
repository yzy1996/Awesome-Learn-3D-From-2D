# <p align=center>`Learn 3D object from 2D images` </p>

A collection of resources on learning 3D object from 2D images.



[toc]

## Introduction

> Alias: image-based 3D reconstruction

==[Impact & sustained attention]== 3D reconstruction from multiple RGB images is a fundamental problem in computer vision with various applications in robotics, graphics, animation, virtual reality, and more. Recently, significant advances have been made towards complete reconstruction (geometry and appearance/texture) from an RGB image input.

==[Problem introduction]== The reconstruction is often accompanied by representation, and the whole process is under the assumptions of known materials, viewpoints, and lighting conditions. If the materials, viewpoints, and lighting are not known, this will be generally an ill-posed problem because combinations of geometry, materials, viewpoints, and lighting can produce exactly the same photographs (**ambiguity**). As a result, without further assumptions, no single algorithm can correctly reconstruct the 3D geometry from photographs alone.

==[Old MVS]== Multi-View Stereo (MVS) methods are a classic branch to solve this tough challenge.

==[Novel neural methods]== Beyond methods of ~~traditional representation~~ (voxel, grid, mesh) and ~~relied on 3D supervision~~, the recent popular approaches utilizing neural implicit representation (coordinate-based neural networks) yeild state-of-the-art performance because they tend to produce **smoothness bias of neural networks**. The key idea behind is to use compact, memory efficient multi-layer perceptrons (MLPs) to parameterize implicit shape representations such as occupancy or signed distance fields (SDF). 

Some works use differentiable <u>surface rendering</u> to reconstruct scenes from multi-view images. Neural radiance fields (NeRFs) achieved impressive novel view synthesis results with <u>volume rendering</u> techniques. Some latest efforts <u>combine surface and volume rendering</u> by expressing volume density as a function of the underlying 3D surface, which in turn improves scene geometry.

==[Goal & future]== The ultimate goal is to infer the underlying geometric structures and identify object and structure semantics, even from a partial, single view observation.



### Problem Statement

given a set of photographs of an object or a scene, estimate the most likely 3D shape that explains those photographs, under the assumptions of known materials, viewpoints, and lighting conditions.

<img src="https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20211121113332.png" alt="image from" style="zoom:50%;" />

Let $\mathbf{I} = \{I_k, k=1, \dots, n\}$ be a set of $n \ge 1$ RGB images of one or multiple objects $X$. 3D reconstruction can be summarized as the process of learning a predictor $f_\theta$ that can infer a shape $\hat{X}$ that is as close as possible to the unknown shape $X$.

The function $f_{\theta}$ is the minimizer of a reconstruction objective $\mathcal{L}(\mathbf{I}) = d(f_\theta (\mathbf{I}), X)$. Here, $d(\cdot)$ is a certain measure of distance between the target shape $X$ and the reconstructed shape $f(\mathbf{i})$.



## Research Branch

> Click to see the details.

- Multi-View 3D Reconstruction
  - Method: [Multi-View Stereo (MVS)](./Multi-View Stereo (MVS))
  - Method: Neural Implicit Volume Reconstruction
  - Method: Neural Implicit Surface Reconstruction

- Novel-View Synthesis (NVS)

- Single-Image Reconstruction (SIR)

- 3D-Aware Generation

- Predict Camera Parameters

- Predict depth



> 生成新视角需要先还原3D shape吗?



### Extra & Aforementioned limitations

large and more complex scenes

scenes captured from sparse viewpoints

The core is ambiguities.

3D semantic reconstruction

instance reconstruction



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

Deep 3D Portrait from a Single Image



