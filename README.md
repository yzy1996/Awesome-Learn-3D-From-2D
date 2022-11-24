# <p align=center>`Learn 3D object from 2D images` </p>

A collection of resources on learning 3D object from 2D images. 

> Alias: image-based 3D reconstruction



## Introduction

**[Impact & sustained attention]** 3D reconstruction from multiple RGB images is a fundamental problem in computer vision with various applications in robotics, graphics, animation, virtual reality, and more. Recently, significant advances have been made towards complete reconstruction (geometry and appearance/texture) from an RGB image input.

**[Problem introduction]** The reconstruction is often accompanied by representation, and the whole process is under the assumptions of known materials, viewpoints, and lighting conditions. If the materials, viewpoints, and lighting are not known, this will be generally an ill-posed problem because combinations of geometry, materials, viewpoints, and lighting can produce exactly the same photographs (**ambiguity**). As a result, without further assumptions, no single algorithm can correctly reconstruct the 3D geometry from photographs alone.

**[Old MVS]** Multi-View Stereo (MVS) methods are a classic branch to solve this tough challenge.

**[Novel neural methods]** Beyond methods of ~~traditional representation~~ (voxel, grid, mesh) and ~~relied on 3D supervision~~, the recent popular approaches utilizing neural implicit representation (coordinate-based neural networks) yeild state-of-the-art performance because they tend to produce **smoothness bias of neural networks**. The key idea behind is to use compact, memory efficient multi-layer perceptrons (MLPs) to parameterize implicit shape representations such as occupancy or signed distance fields (SDF). 

Some works use differentiable <u>surface rendering</u> to reconstruct scenes from multi-view images. Neural radiance fields (NeRFs) achieved impressive novel view synthesis results with <u>volume rendering</u> techniques. Some latest efforts <u>combine surface and volume rendering</u> by expressing volume density as a function of the underlying 3D surface, which in turn improves scene geometry.

**[Goal & future]** The ultimate goal is to infer the underlying geometric structures and identify object and structure semantics, even from a partial, single view observation.



### Problem Statement

given a set of photographs of an object or a scene, estimate the most likely 3D shape that explains those photographs, under the assumptions of known materials, viewpoints, and lighting conditions.

<img src="https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20211121113332.png" alt="image from" style="zoom:50%;" />

Multi-View Stereo: A tutorial

Let $\mathbf{I} = \{I_k, k=1, \dots, n\}$ be a set of $n \ge 1$ RGB images of one or multiple objects $X$. 3D reconstruction can be summarized as the process of learning a predictor $f_\theta$ that can infer a shape $\hat{X}$ that is as close as possible to the unknown shape $X$.

The function $f_{\theta}$ is the minimizer of a reconstruction objective $\mathcal{L}(\mathbf{I}) = d(f_\theta (\mathbf{I}), X)$. Here, $d(\cdot)$ is a certain measure of distance between the target shape $X$ and the reconstructed shape $f(\mathbf{i})$.



The futher problem is recover a 3D shape with texture and mesh from a single view observation. This need utilize a pre-trained 3D GAN by searching for a latent space that best resembles the target mesh. As we all know that the pre-trained GAN encapsulates rich 3D semantics in terms of mesh geometry and texture, searching within the GAN manifold thus naturally regularizes the realness and fidelity of the reconstruction.



## Research Branch

> Click subfolders to see the rich literatures and details. 

- Multi-View 3D Reconstruction
  - Method: [Multi-View Stereo (MVS)](./Multi-View%20Stereo%20(MVS))
  - Method: [3D representation](./3D%20Representation%20and%20Reconstruction)
- [Novel-View Synthesis (NVS)](./Novel-View%20Synthesis%20(NVS))
- [Single View Reconstruction](./Single%20View%20Reconstruction)
- [3D-Aware-Generation](./3D-Aware-Generation)
- [Predict Camera & Depth](./Predict%20Camera%20&%20Depth)



### Limitations

- large and more complex scenes

- scenes captured from sparse viewpoints

- the core is ambiguities.

- 3D semantic reconstruction

- instance reconstruction



