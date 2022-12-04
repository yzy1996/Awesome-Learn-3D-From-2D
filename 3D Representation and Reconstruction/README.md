# <p align=center>`3D Representation & Reconstruction `</p>

A collection of resources on 3D representation and reconstruction from multi-view images. Finding a proper way to capture and store 3D scene.

> 表征是为了干什么，那肯定是为了重建，所以两者不分家。其中表征就是一个Encoder，重建就是一个Decoder。仅仅重建又不是不够的，还需要能够生成新的



**Related project:** [subeeshvasu/Awsome_Deep_Geometry_Learning](https://github.com/subeeshvasu/Awsome_Deep_Geometry_Learning) | [vsitzmann/awesome-implicit-representations](https://github.com/vsitzmann/awesome-implicit-representations) | [yenchenlin/awesome-NeRF](yenchenlin/awesome-NeRF) | [weihaox/awesome-neural-rendering](weihaox/awesome-neural-rendering)



## Introduction

Our goal is to **reconstruct 3D objects or scenes** (geometry and appearance) from **single or multiple posed 2D images**, by means of one of the **3D representation methods** (e.g., point cloud, neural implicit function, surface).  With this naturally comes the application of **3D obejct surface reconstruction** and **novel views synthesis** by **rendering**.

> 其实除了从 2D image 里学，输入数据还可以是PointCloud，或者RGB-D Images。
>
> [representation 3D shape] in an **accurate**, **efficient** and **compact** manner

因为真实世界是3D的，所以我们希望能够表征和重建3D模型，另一方面3D表征带来的优势是 和视角无关的，这为机器人环境探索，行人重识别带来了便利。

这里我主要关注的是 implicit neural functions 这一类方法，就是用神经网络来表征3D几何，也可以被称为 coordinate-based neural models，因为是建立了空间中的点到某一指标（feature）的映射关系；Occupancy Field 和 SDF 是映射到 Surface 值，NeRF 是映射到 不透明度和颜色。这一类方法具有的特点是：全空间连续可导 (分辨率可以无限大)，表征能力强大，占用内存小。因为是用神经网络的权重表征的，所以可以结合例如meta-learning学习一个可泛化的先验。

> 对比的是一些显式表征，例如 point cloud, mesh, voxels。过去这些方法的训练是需要3D监督的，因为是和这些监督真值去对比，而隐式表征因为都是可导的，所以可以借助神经网络的反向传播直接和输入真值去对比，做到end-to-end。这需要依靠 neural rendering。

这些神经隐式表征方法还需要额外的配套渲染技术，渲染可以简单理解为“对3D模型拍个照得到2D图像”，复杂一点讲需要涵盖 cameras pose, lights, surface geometry and material 这么多因素。神经网络的学习靠的就是渲染后的图片和原图进行对比。use a rendering method to render a 3D object into images and use the rendered images to compare against input images for supervision.

通常学习的过程中很难做到单张图训练，学习到足够的先验信息后再通过逆向渲染做到对单张图的推断。在做的过程中，为了简化，我们也会使用canonical view / model。

The application varies from robotics, 3D modeling, to virtual reality, etc.

Learning the prior descriptors or prototypes from a large scale dataset is a long-studied topic.



当我们在谈论一个2D object 的时候，一幅图像的载体就是像素值 pixel，先不去想彩色图，甚至不是灰度图，而就是黑白图，也就是经过二值化后的灰度图。是不是就能知道这个object的形状。

而3D object，载体可以是体素值（类比像素值）voxel grids；为什么是可以是，因为还可以是point clouds，meshes。为什么呢，因为看到他们我们也可以知道这个object的形状呀。这些表征的特点是：**离散**，对complex geometry 的 fidelity **（保真度）高**。



首先划分为 是表征**单个物体** 还是表征**一个类别的物体**

其次划分为 不同的表征方法 **explicit** and **implicit**

主要解决的问题 multi-view consistency and object parts occluded encode **geometry** and **appearance** 

there is no canonical representation which is both computationally and memory efficient for high-resolution 3D representation . Given 2D image observations, these approaches aim to infer a 3D-structure-aware representation of the underlying scene that enables prior based predictions about occluded parts.

少不了比较，显式的可以很容易转换到2D图像，缺点是 分辨率有限 Fidelity， 或者 无法表达拓扑结构 Topology

隐式的可以解决上面这两个问题，但不好渲染到2D图



## Research Branch

> Click subfolders to see the rich literatures and details. 

- [Explicit Representation](./1-Explicit%20Representation)
- [Implicit Neural Representation](./2-Implicit%20Neural%20Representation%20(INR))
- [Neural Rendering](./3-Neural%20Rendering)
- [Other Applications](./Other%20Applications)



先对主要方法进行一个分类：

- Explicit Representation
  - Voxels (large memory cost, limiting the output resolution)
  - Point Clouds (sparse, lack the connectivity structure and hence require additional post processing steps to extra 3D geometry from the model.)
  - Polygonal Meshes (based on forming a template mesh)
- Implicit Representation (continues, arbitrary resolution)
  - Implicit Surface
    - occupancy Function
    - Signed Distance Function
  - Implicit Volume
    - Neural Radiance Field



**Voxel based**：因为它可以直接类比2D的像素，到了3D就成了体素，因此很多传统的2D 卷积网络可以直接迁移过来，同时拓扑结构也很好泛化迁移；但是由于很占内存，分辨率无法很高。

**Point based**：通过 point feature 是可以从2D 图重建点云的，点云也有很好的拓扑结构；但依然被采样限制了分辨率。

**Mesh based**：（可以从点云和2D数据重建mesh）做到了是稠密的，解决了分辨率的限制，但因为都是多边形线条网格，很难确定物体的形状顶点，也就是拓扑性不够好。

**Implicit Surface**：得提取 iso-surface 等势面



Unlike explicit representations of geometry, neural implicit methods are memory efficient and are able to capture impressive levels of geometric detail.

In contrast to traditional multi-view stereo algorithms, learned models are able to encode rich prior information about the space of 3D shapes which helps to resolve ambiguities in the input.

computationally expensive since it requires many forward passes through the network for every pixel.



尽可能花费少地

- 重建 reconstruction, 尽可能少的角度输入图像，最理想的是一张图片即可。a handful of views or ideally just one view.
- 直接对3D数据开展识别这样的task



表征的方式一般有：

- Volumetric (OctNet)
- PointClouds (PointSetGen)
- Surfaces (AtlasNet)
- Signed / Unsigned Distance Function
- Geometeric Primitives
- occupancy field
- depth maps
- implicit functions



**Some related keywords:** represent appearance and 3D geometry information | per-point semantic segmentation 



### Data

- [**ShapeNets**](https://shapenet.org/)  
  [3D ShapeNets: A Deep Representation for Volumetric Shapes](https://arxiv.org/pdf/1406.5670.pdf)  
  **[`CVPR 2015`] (`Princeton, CUH, MIT`)**  
  *Zhirong Wu, Shuran Song, Aditya Khosla, Fisher Yu, Linguang Zhang, Xiaoou Tang, Jianxiong Xiao*

- [**CO3D**](https://github.com/facebookresearch/co3d) by Facebook  
  [Common Objects in 3D: Large-Scale Learning and Evaluation of Real-life 3D Category Reconstruction](https://arxiv.org/pdf/2109.00512)  
  *Jeremy Reizenstein, Roman Shapovalov, Philipp Henzler, Luca Sbordone, Patrick Labatut, David Novotny*  
  **[` ICCV 2021`]**



[Google Scanned Objects](https://app.gazebosim.org/GoogleResearch/fuel/collections/Google%20Scanned%20Objects) by Google



**MVS Datasets**

Middlebury MVS

EPFL benchmark

DTU dataset

Tanks and Temples benchmark

ETH3D benchmark
