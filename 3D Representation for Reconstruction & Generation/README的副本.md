# <p align=center>`3D representation & reconstruction` </p>

A collection of resources on 3D representation and reconstruction from multi-view images. Finding a proper way to capture and store 3D scene.

> 表征是为了干什么，那肯定是为了重建，所以两者不分家。其中表征就是一个Encoder，重建就是一个Decoder。仅仅重建又不是不够的，还需要能够生成新的



**Related project:**

[vsitzmann/awesome-implicit-representations](https://github.com/vsitzmann/awesome-implicit-representations)

[yenchenlin/awesome-NeRF](yenchenlin/awesome-NeRF)

[weihaox/awesome-neural-rendering](weihaox/awesome-neural-rendering)



**News:** 

Latest 3D dataset:

[CO3D](https://ai.facebook.com/datasets/co3d-downloads/) by Facebook

[Google Scanned Objects](https://app.gazebosim.org/GoogleResearch/fuel/collections/Google%20Scanned%20Objects) by Google



## Table of Contents

- [3D Representation](#3D-Representation) (一些3D表征的方法)
  - [Point Cloud](./1-3D-Representation/Point-Cloud), [Meshes](./1-3D-Representation/Meshes), [Voxels](./1-3D-Representation/Voxels), Neural Implicit Functions (except NeRF)
- [Rendering](#Rendering) (有了表征当然就要有渲染)
  - [Surface Rendering](./2-Rendering/Surface-Rendering), [Volume Rendering](./2-Rendering/Volume-Rendering)

- [NeRF](#NeRF) (因为太火爆，所以给 NeRF related 开个专门的话题)
- [Neural Rendering](#Neural-Rendering) (这是一个很大的话题，因此把不好划分到上述的归类到这里)
  - [Inverse Rendering](./4-Neural-Rendering/Inverse-Rendering), [Relight](./4-Neural-Rendering/Relight), [Single View Reconstruction](./4-Neural-Rendering/Single-View-Reconstruction), Shape Completion
- [Tricks](#Tricks) 
  - SIREN
- [Datasets](#Datasets)



Survey



## 1. Introduction

Our goal is to **reconstruct 3D objects or scenes** (geometry and appearance) from **single or multiple posed 2D images**, by means of one of the **3D representation methods** (e.g., point cloud, neural implicit function, surface).  With this naturally comes the application of **3D obejct surface reconstruction** and **novel views synthesis** by **rendering**.

> 其实除了从 2D image 里学，输入数据还可以是PointCloud，或者RGB-D Images。



Recently, implicit neural representation (INR) which … has been driving significant advantages in solving this task.

spatial coordinate information is insufficient for the network to learn a continuous 3D representation with limited input.

what we can do is to enrich the representation of each coordinate and compensate for the missing information when only sparse views are provided. It’s pritical to overcome this drawback by 



Learning the prior descriptors or prototypes from a large scale dataset is a long-studied topic 





因为真实世界是3D的，所以我们希望能够表征和重建3D模型，另一方面3D表征带来的优势是 和视角无关的，这为机器人环境探索，行人重识别带来了便利。

这里我主要关注的是 implicit neural functions 这一类方法，就是用神经网络来表征3D几何，也可以被称为 coordinate-based neural models，因为是建立了空间中的点到某一指标（feature）的映射关系；Occupancy Field 和 SDF 是映射到 Surface 值，NeRF 是映射到 不透明度和颜色。这一类方法具有的特点是：全空间连续可导 (分辨率可以无限大)，表征能力强大，占用内存小。因为是用神经网络的权重表征的，所以可以结合例如meta-learning学习一个可泛化的先验。

> 对比的是一些显式表征，例如 point cloud, mesh, voxels。过去这些方法的训练是需要3D监督的，因为是和这些监督真值去对比，而隐式表征因为都是可导的，所以可以借助神经网络的反向传播直接和输入真值去对比，做到end-to-end。这需要依靠 neural rendering。

这些神经隐式表征方法还需要额外的配套渲染技术，渲染可以简单理解为“对3D模型拍个照得到2D图像”，复杂一点讲需要涵盖 cameras pose, lights, surface geometry and material 这么多因素。神经网络的学习靠的就是渲染后的图片和原图进行对比。use a rendering method to render a 3D object into images and use the rendered images to compare against input images for supervision.

通常学习的过程中很难做到单张图训练，学习到足够的先验信息后再通过逆向渲染做到对单张图的推断。在做的过程中，为了简化，我们也会使用canonical view / model。



> Multi-view stereo (MVS) reconstructs the dense representation of the scene from multi-view images and corresponding camera parameters. also summarized as ‘multi-view posed images’

The application varies from robotics, 3D modeling, to virtual reality, etc.



可以坐在家里，仅通过一张图片还原当时场景，不需要受限于场景空间，视角是自由的

nerf++



novel view synthesis task

coordinate based MLPs



## 2. 3D Representation

首先划分为 是表征**单个物体** 还是表征**一个类别的物体**

其次划分为 不同的表征方法 explicit and implicit



但似乎是某些特定的方法专门研究出来表征一个类别物体的



当我们在谈论一个2D object 的时候，一幅图像的载体就是像素值 pixel，先不去想彩色图，甚至不是灰度图，而就是黑白图，也就是经过二值化后的灰度图。是不是就能知道这个object的形状。

而3D object，载体可以是体素值（类比像素值）voxel grids；为什么是可以是，因为还可以是point clouds，meshes。为什么呢，因为看到他们我们也可以知道这个object的形状呀。这些表征的特点是：**离散**，对complex geometry 的 fidelity **（保真度）高**。


### 2.1 Explicit


#### PointCloud

- [A Point Set Generation Network for 3D Object Reconstruction from a Single Image](https://arxiv.org/pdf/1612.00603.pdf)  
  **[`CVPR 2017`] (`Tsinghua, Stanford`)**  
  *Haoqiang Fan, Hao Su, Leonidas Guibas*

- [PointNet: Deep Learning on Point Sets for 3D Classification and Segmentation](https://arxiv.org/pdf/1612.00593.pdf)  
  **[`CVPR 2017`] (`Stanford`)**  
  *Charles R. Qi, Hao Su, Kaichun Mo, Leonidas J. Guibas*

- [PointNet++: Deep Hierarchical Feature Learning on Point Sets in a Metric Space](https://arxiv.org/pdf/1706.02413.pdf)  
  **[`NeurIPS 2017`] (`Stanford`)**  
  Charles R. Qi, Li Yi, Hao Su, Leonidas J. Guibas

- [Large-scale point cloud semantic segmentation with superpoint graphs](https://arxiv.org/pdf/1711.09869.pdf)  
  **[`CVPR 2018`] (`Universite Paris-Est`)**  
  *Loic Landrieu, Martin Simonovsky*

---

#### Mesh

- [Pixel2Mesh Generating 3D Mesh Models from Single RGB Images](https://arxiv.org/pdf/1804.01654.pdf)  
  **[`ECCV 2018`] (`Fudan, Princeton`)**  
  *Nanyang Wang, Yinda Zhang, Zhuwen Li, Yanwei Fu, Wei Liu, Yu-Gang Jiang*

- [Meshlet Priors for 3D Mesh Reconstruction](https://arxiv.org/pdf/2001.01744.pdf)  
  **[`CVPR 2020`] (`NVIDIA, UCSB`)**  
  *Abhishek Badki, Orazio Gallo, Jan Kautz, Pradeep Sen*

---

#### Voxels

优点：由像素直接上升到体素，很多2D的方法可以直接迁移过来

缺点：curse of dimensionality

- [3D-R2N2: A Unified Approach for Single and Multi-view 3D Object Reconstruction](https://arxiv.org/pdf/1604.00449.pdf)  
  **[`ECCV 2016`] (`Stanford`)**  
  *Christopher B. Choy, Danfei Xu, JunYoung Gwak, Kevin Chen, Silvio Savarese*

- [Voxnet: A 3d convolutional neural network for real-time object recognition](https://www.ri.cmu.edu/pub_files/2015/9/voxnet_maturana_scherer_iros15.pdf)  
  **[`IROS 2015`] (CMU)**  
  *Daniel Maturana, Sebastian Scherer*

- [Octnet: Learning deep 3d representations at high resolutions](https://arxiv.org/pdf/1611.05009.pdf)  
  **[`CVPR 2017`] (`Graz University of Technology, MPI, ETH`)**  
  *Gernot Riegler, Ali Osman Ulusoy, Andreas Geiger*

- [Octnetfusion: Learning depth fusion from data](https://arxiv.org/pdf/1704.01047.pdf)  
  **[`3DV 2017`] (`Graz University of Technology, MPI, ETH`)**  
  *Gernot Riegler, Ali Osman Ulusoy, Horst Bischof, Andreas Geiger*

---



### Neural Implicit Function

先回顾一下在还没引入 Deep Learning 之前的历史，属于 classic multi-view stereo (**MVS**) methods. They mainly focus on either matching features across views or representing shapes with a voxel grid. The former  approaches need a complex pipeline rquiring additional steps like fusing depth information and meshing. The latter ones are limited to low resolution due to cubic memory requirements.

鉴于此，引入了 neural implicit representations, 完全连续，用起来简单，占用内存小。



SDF 和 occupancy probabulity 这一大类因为训练的 truth ground是真实的3D 数据，和后面的 without 3D supervision 还不太一样。这一类可以被称为 Neural Implicit Surface。

#### Occupancy and Signed Distance Function

缺点：bad on sharp areas，需要3D监督信号，因为不需要differentiable renderer

- [Implicit surface representations as layers in neural networks](https://openaccess.thecvf.com/content_ICCV_2019/papers/Michalkiewicz_Implicit_Surface_Representations_As_Layers_in_Neural_Networks_ICCV_2019_paper.pdf)  
  **[`ICCV 2019`] (`Queensland`)**  
  *Mateusz Michalkiewicz, Jhony K. Pontes, Dominic Jack, Mahsa Baktashmotlagh, Anders Eriksson*
- [(IM-NET)Learning Implicit Fields for Generative Shape Modeling](https://arxiv.org/pdf/1812.02822.pdf)  
  **[`CVPR 2019`] (`Simon Fraser University`)**  
  *Zhiqin Chen, Hao Zhang*
- [Occupancy Networks: Learning 3D Reconstruction in Function Space](https://arxiv.org/pdf/1812.03828.pdf)  
  **[`CVPR 2019`] (`MPI, Google`)**  
  *Lars Mescheder, Michael Oechsle, Michael Niemeyer, Sebastian Nowozin, Andreas Geiger*
- [DeepSDF: Learning Continuous Signed Distance Functions for Shape Representation](https://arxiv.org/pdf/1901.05103.pdf)  
  **[`CVPR 2019`] (`UW, MIT`)**  
  *Jeong Joon Park, Peter Florence, Julian Straub, Richard Newcombe, Steven Lovegrove*
- [PIFu: Pixel-Aligned Implicit Function for High-Resolution Clothed Human Digitization](https://arxiv.org/pdf/1905.05172.pdf)  
  **[`ICCV 2019`] (`USC, Pinscreen`)**  
  *Shunsuke Saito, Zeng Huang, Ryota Natsume, Shigeo Morishima, Angjoo Kanazawa, Hao Li*

---

surface-based, volume-based

下面是用 implicit function + neural rendering 中隐式表征的通用形式：

$$
F_{\theta}:(\boldsymbol{p}, \boldsymbol{v}) \rightarrow (\boldsymbol{c}, \omega)
$$
where $\theta$ is parameters of an underlying neural network, $\boldsymbol{p}$ is the scene color, $\omega$ is the probility density (opacity) at spatial location $\boldsymbol{p}$, $\boldsymbol{v}$ is the ray direction. We can render a 2D image by shooting rays from a pin-hole camera   position $\boldsymbol{p}_0 \in \mathbb{R}^3$ to the 3D scene. The spatial location along the camera ray can be represented by $\boldsymbol{p}(z)=\boldsymbol{p}_{0}+z \cdot \boldsymbol{v}$. Note that $\omega$ is restricted only by $\boldsymbol{p}(z)$ while $\boldsymbol{c}$ is affected by both $\boldsymbol{p}$ and $\boldsymbol{v}$​ to model view-dependent color. 



**surface rendering**

assume $\omega(\boldsymbol{p}(z))$ to be Dirac function $\delta(\boldsymbol{p}(z) - \boldsymbol{p}(z^*))$​ where $\boldsymbol{p}(z^*)$ is the intersection of the camera ray with the scene geometry.

> 需要找到准确的 surface，才能让颜色保持多角度的一致性
>
> 不然会导致模糊

Scene representation networks

Dist: Rendering deep implicit signed distance function with differentiable sphere tracing

Differentiable: volumetric rendering: Learning implicit 3d representations without 3d supervision



**volume rendering**
$$
C\left(\boldsymbol{p}_{0}, \boldsymbol{v}\right)=\int_{0}^{+\infty} \omega(\boldsymbol{p}(z)) \cdot \boldsymbol{c}(\boldsymbol{p}(z), \boldsymbol{v}) d z, \quad \text { where } \int_{0}^{+\infty} \omega(\boldsymbol{p}(z)) d z=1
$$

> Volume rendering methods need to sample a high number of points along the rays for color accumulation to achieve high quality rendering. This rendering is realized through integral projection.

Neural volumes: Learning dynamic renderable volumes from images

Nerf: Representing scenes as neural radiance fields for view synthesis

 

#### Surface Reconstruction

优点：

缺点：

Regard the object surface as a 2-dimensional manifold embedded in the 3-dimensional space.

- [AtlasNet: A Papier-Mâché Approach to Learning 3D Surface Generation](https://arxiv.org/pdf/1802.05384.pdf)  
  **[`CVPR 2018`] (`LIGM, Adobe`)**  
  *Thibault Groueix, Matthew Fisher, Vladimir G. Kim, Bryan C. Russell, Mathieu Aubry*
- [Learning to Infer Implicit Surfaces without 3D Supervision](https://arxiv.org/pdf/1911.00767.pdf)  
  **[`NeurIPS 2019`] (`USC`)**  
  *Shichen Liu, Shunsuke Saito, Weikai Chen, Hao Li*
- [Scene Representation Networks: Continuous 3D-Structure-Aware Neural Scene Representations](https://arxiv.org/pdf/1906.01618.pdf)  
  **[`NeurIPS 2019`] (`Stanford`)**  
  *Vincent Sitzmann, Michael Zollhöfer, Gordon Wetzstein*
- [Analytic Marching: An Analytic Meshing Solution from Deep Implicit Surface Networks]()  
  **[`ICML 2020`] (`SCUT`)**  
  *Jiabao Lei, Kui Jia*

> 这里补充一点是，可以用 Marching cubes 从SDF 得到Mesh



[Sdfdiff: Differentiable rendering of signed distance fields for 3d shape optimization](https://arxiv.org/pdf/1912.07109.pdf)  
**[`CVPR 2020`] (`University of Maryland`)**  
*Yue Jiang, Dantong Ji, Zhizhong Han, Matthias Zwicker*



## Rendering

> for more details see [folder](./2-Rendering)

这里关心的是神经渲染这一类，因为要和神经表征去搭配。主要的方法是 rasterization and raytracing

- volume rendering

  integrate densities by drawing samples along the viewing rays

- surface rendering

  Differentiable volumetric rendering (DVR)

  Multiview neural surface reconstruction (IDR)



fast rendering

- [Fast Training of Neural Lumigraph Representations using Meta Learning](https://arxiv.org/pdf/2106.14942.pdf)  
  **[`Arxiv 2021`] (`Stanford`)**  
  Alexander W. Bergman, Petr Kellnhofer, Gordon Wetzstein



### Marching Cubes

- [Deep marching cubes: Learning explicit surface representations](http://www.cvlibs.net/publications/Liao2018CVPR.pdf)  
  **[`CVPR 2018`] (MPI, Zhejiang U)**  
  *Yiyi Liao, Simon Donné, Andreas Geiger*

- [Marching cubes: A high resolution 3D surface construction algorithm](https://people.eecs.berkeley.edu/~jrs/meshpapers/LorensenCline.pdf)  
  **[`SIGGRAPH 1987`] (`General Electric Company`)**  
  *William E. Lorensen, Harvey E. Cline*



## NeRF

> for more details see [folder](./3-NeRF)



### Enhance NeRF

data structures

- [PlenOctrees for real-time rendering of neural radiance fields](https://arxiv.org/pdf/2103.14024.pdf)  
  **[`Arxiv 2021`] (`UCB`)**  
  *Alex Yu, Ruilong Li, Matthew Tancik, Hao Li, Ren Ng, Angjoo Kanazawa*
- [Baking neural radiance fields for real-time view synthesis](https://arxiv.org/pdf/2103.14645.pdf)  
  **[`Arxiv 2021`] (`Google`)**  
  *Peter Hedman, Pratul P. Srinivasan, Ben Mildenhall, Jonathan T. Barron, Paul Debevec*

pruning

- [Neural sparse voxel fields](https://arxiv.org/pdf/2007.11571.pdf)  
  **[`NeurIPS 2020`] (`MPI`)**  
  *Lingjie Liu, Jiatao Gu, Kyaw Zaw Lin, Tat-Seng Chua, Christian Theobalt*

importance sampling

- [DONeRF: Towards Real-Time Rendering of Compact Neural Radiance Fields using Depth Oracle Networks](https://arxiv.org/pdf/2103.03231.pdf)  
  **[`EGSR 2021`] (`Graz University of Technology`)**  
  *Thomas Neff, Pascal Stadlbauer, Mathias Parger, Andreas Kurz, Joerg H. Mueller, Chakravarty R. Alla Chaitanya, Anton Kaplanyan, Markus Steinberger*

fast integration

- [Autoint: Automatic integration for fast neural volume rendering](https://arxiv.org/pdf/2012.01714.pdf)  
  **[`CVPR 2021`] (`Stanford`)**  
  *David B. Lindell, Julien N. P. Martel, Gordon Wetzstein*



### NeRF + Surface

- [UNISURF: Unifying Neural Implicit Surfaces and Radiance Fields for Multi-View Reconstruction](https://arxiv.org/pdf/2104.10078.pdf)  
  **[`Arxiv 2021`] (`MPI`)**  
  *Michael Oechsle, Songyou Peng, Andreas Geiger*



## Neural Rendering

> for more details see [folder](./4-Neural-Rendering)
>
> neural rendering 包含了 NeRF，指的是用 神经表征和渲染 的一类方法，它是一类方法或者技术的总称。
>
> The goal of neural rendering is to project a 3D neural scene representation into one or multiple 2D images.
>
> 简单说neural rendering可以涵盖所有新的带neural的技术









### Single View Reconstruction (SVR)

> 从单张图像重建整个3D场景是很重要的一个话题，more details see [file](./Single-View-Reconstruction)
>
> 也可以叫 single image reconstruction，对一个 3D 目标，单个图像就是单个视角

- [Unsupervised Learning of Probably Symmetric Deformable 3D Objects from Images in the Wild](https://arxiv.org/pdf/1911.11130.pdf)  
  **[`CVPR 2020`]  (`Oxford`)**  
  *Shangzhe Wu, Christian Rupprecht, Andrea Vedaldi*
- [Learning Shape Priors for Single-View 3D Completion and Reconstruction](https://arxiv.org/pdf/1809.05068.pdf)  
  **[`ECCV 2018`] (`MIT`)**  
  *Jiajun Wu, Chengkai Zhang, Xiuming Zhang, Zhoutong Zhang, William T. Freeman, Joshua B. Tenenbaum*

### Shape Completion

> estimates the complete geometry from a partial shape



Unsupervised 3D Shape Completion through GAN Inversion





## Tricks

> for more details see [folder](./5-Tricks) 

**Issue**:

standard ReLU MLPs fail to adequately represent fine details in these complex low-dimensional signals due to a spectral bias

**Solution**:

- replace the ReLU activations with sine functions
- lift the input coordinates into a Fourier feature space 



## Datasets

- [**ShapeNets**](https://shapenet.org/)  
  [3D ShapeNets: A Deep Representation for Volumetric Shapes](https://arxiv.org/pdf/1406.5670.pdf)  
  **[`CVPR 2015`] (`Princeton, CUH, MIT`)**  
  *Zhirong Wu, Shuran Song, Aditya Khosla, Fisher Yu, Linguang Zhang, Xiaoou Tang, Jianxiong Xiao*

- [**CO3D**](https://github.com/facebookresearch/co3d)  
  [Common Objects in 3D: Large-Scale Learning and Evaluation of Real-life 3D Category Reconstruction](https://arxiv.org/pdf/2109.00512)  
  *Jeremy Reizenstein, Roman Shapovalov, Philipp Henzler, Luca Sbordone, Patrick Labatut, David Novotny*  
  **[` ICCV 2021`] (``)**





**MVS Datasets**

Middlebury MVS

EPFL benchmark

DTU dataset

Tanks and Temples benchmark

ETH3D benchmark



数量需要足够多



**Synthetic Datasets**

