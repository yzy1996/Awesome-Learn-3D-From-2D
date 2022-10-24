# <p align=center>`3D Scenes Representation `</p>

related project: [Awsome_Deep_Geometry_Learning](https://github.com/subeeshvasu/Awsome_Deep_Geometry_Learning)



capture and store 3D scenes

为什么要做3D 表征

如果仅仅是表征一张2D图片，那怎么刻画不同角度，没有见过的角度，以及遮挡呢

multi-view consistency 

object parts occluded 

## Introduction

> **Challenge Description**

[representation 3D shape] in an **accurate**, **efficient** and **compact** manner



there is no canonical representation which is both computationally and memory efficient for high-resolution 3D representation 



encode **geometry** and **appearance** 



Unlike explicit representations of geometry, neural implicit methods are memory efficient and are able to capture impressive levels of geometric detail.



先对主要方法进行一个分类：

- Explicit Representation
  - Voxels
  - Point Clouds
  - Polygonal Meshes
- Implicit Representation
  - Implicit Surface
    - occupancy function
    - signed distance function
  - Implicit Volume
    - Neural Radiance Field



少不了比较，显式的可以很容易转换到2D图像，缺点是 分辨率有限 Fidelity， 或者 无法表达拓扑结构 Topology

隐式的可以解决上面这两个问题，但不好渲染到2D图

 

**Voxel based**：因为它可以直接类比2D的像素，到了3D就成了体素，因此很多传统的2D 卷积网络可以直接迁移过来，同时拓扑结构也很好泛化迁移；但是由于很占内存，分辨率无法很高。

**Point based**：通过 point feature 是可以从2D 图重建点云的，点云也有很好的拓扑结构；但依然被采样限制了分辨率。

**Mesh based**：（可以从点云和2D数据重建mesh）做到了是稠密的，解决了分辨率的限制，但因为都是多边形线条网格，很难确定物体的形状顶点，也就是拓扑性不够好。



**Implicit Surface**：得提取 iso-surface 等势面







volume-based 

surface-based 

> Pixels, voxels, and views: A study of shape representations for single view 3D object shape prediction



> In contrast to traditional multi-view stereo algorithms, learned models are able to encode rich prior information about the space of 3D shapes which helps to resolve ambiguities in the input. [Occupancy](#Occupancy)



computationally expensive since it requires many forward passes through the network for every pixel.



表征的目的：



尽可能花费少地

- 重建 reconstruction, 尽可能少的角度输入图像，最理想的是一张图片即可。a handful of views or ideally just one view.
- 直接对3D数据开展识别这样的task
- 





From a data structure point of view, a point cloud is an unordered set of vectors. While most work in deep learning focus on regular input representations like sequences, images and volumes.





signed distance functions   occupancy networks 





表征的方式一般有：

- Volumetric (OctNet)
- PointClouds (PointSetGen)
- Surfaces (AtlasNet)
- Signed / Unsigned Distance Function
- Geometeric Primitives
- occupancy field
- depth maps
- implicit functions





现有的表征模型有：

- voxel grids

  large memory cost, limiting the output resolution

- point cloud

  表征是稀疏的, lack the connectivity structure and hence require additional post processing steps to extra 3D geometry from the model.

- mesh

  based on forming a template mesh 

  

- implicit field

continues, arbitrary resolution

 

implicit representations encode a scene in the weights of a neural network which can be queried at any coordinate to produce these same scene properties



represent appearance and 3D geometry information 

per-point semantic segmentation 



典型论文以及

探讨一下优缺点



Given 2D image observations, these approaches aim to infer a 3D-structure-aware representation of the underlying scene that enables prior based predictions about occluded parts.



[Neural Sparse Voxel Fields](https://arxiv.org/pdf/2007.11571.pdf)  
**[`NeurIPS 2020`] (`MPI, Facebook`)**  
*Lingjie Liu, Jiatao Gu, Kyaw Zaw Lin, Tat-Seng Chua, Christian Theobalt*



