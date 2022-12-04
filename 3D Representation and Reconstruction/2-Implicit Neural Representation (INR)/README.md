# <p align=center>`Implicit Neural Representation` </p>

[Talk: Neural Implicit Representations for 3D Vision by Dr. Andreas Geiger](https://www.youtube.com/watch?v=jennURL-gtQ)

[awesome-implicit-representations](https://github.com/vsitzmann/awesome-implicit-representations)

## 1. Introduction


<details><summary>杂</summary>
<p>

NeRF 等一系列方法需要稠密的视角输入（50-150张），因此如何松弛这个要求就是需要解决的目标
大类名称叫 coordinate-based neural models ，具体方法叫 neural implicit functions (parameterized with neural networks)，然后又分化成 SDF, occupancy field, radiance field。positional encoding

implicit representations encode a scene in the weights of a neural network which can be queried at any coordinate to produce these same scene properties

先回顾一下在还没引入 Deep Learning 之前的历史，属于 classic multi-view stereo (**MVS**) methods. They mainly focus on either matching features across views or representing shapes with a voxel grid. The former  approaches need a complex pipeline rquiring additional steps like fusing depth information and meshing. The latter ones are limited to low resolution due to cubic memory requirements.

鉴于此，引入了 neural implicit representations, 完全连续，用起来简单，占用内存小。

SDF 和 occupancy probabulity 这一大类因为训练的 truth ground是真实的3D 数据，和后面的 without 3D supervision 还不太一样。这一类可以被称为 Neural Implicit Surface。

</p></details>

---

[INR-GAN] The original idea of augmenting neural networks with coordinates information was proposed in CPPN. The largest popularity of INRs is observed in 3D deep learning, where it provides a cheap and continuous way to represent a 3D shape compared to mesh/voxel/pointcloud-based ones.

**Implicit Neural Representation (INR)** is a promising new avenue of representing general signals by learning a continuous function that, parameterized as a neural network (MLP), maps the domain of a signal to its codomain; the mapping from spatial coordinates of an image to its pixel values, for example.

Instead of storing the signal values corresponding to the coordinate grid, this method train a neural network with continuous activation functions to approximate the coordinate-to-value mapping.

It's a powerful tool for reconstructing 3D structure from multi-view 2D supervision via fitting their 3D models to the multi-view images using differentiable rendering.

Implicit neural representations are a new and promising method to represent images and scenes.

## 2. Research Branches

> Please click the subfolders to see the literatures and details.

- [Neural Radiance Fields (NeRF)](./Neural%20Radiance%20Fields%20(NeRF))
- [Neural Surface Fields](./Neural%20Surface%20Fields)
- [Deep Implicit Templates](./Deep%20Implicit%20Templates)
- [Tricks](./Tricks)
  - Finding an efficient way to encode coordinates positions
  - Be capable of conveying fine details in a high dimensional signal

- Others
  - [+Meta Initialization](./+Meta)
  

## 3. Literature

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



- [Learning Implicit Fields for Generative Shape Modeling](https://arxiv.org/abs/1812.02822)  
  **[`CVPR 2019`]** *Zhiqin Chen, Hao Zhang*  
- [Occupancy Networks: Learning 3D Reconstruction in Function Space](https://arxiv.org/abs/1812.03828)  
  **[`CVPR 2019`]** *Lars Mescheder, Michael Oechsle, Michael Niemeyer, Sebastian Nowozin, Andreas Geiger*  
- [SDFDiff: Differentiable Rendering of Signed Distance Fields for 3D Shape Optimization](https://arxiv.org/abs/1912.07109)  
  **[`CVPR 2020`]** *Yue Jiang, Dantong Ji, Zhizhong Han, Matthias Zwicker*  
- [From Uniform Continuity to Absolute Continuity](https://arxiv.org/abs/1011.6471)  
  **[`arXiv 2010`]** *Kai Yang, Chenhong Zhu*
- [HVTR: Hybrid Volumetric-Textural Rendering for Human Avatars](https://arxiv.org/abs/2112.10203)  
  **[`3DV 2022`]** *Tao Hu, Tao Yu, Zerong Zheng, He Zhang, Yebin Liu, Matthias Zwicker*  
- [Why neural networks find simple solutions: the many regularizers of geometric complexity](https://arxiv.org/abs/2209.13083)  
**[`NeurIPS 2022`]** *Benoit Dherin, Michael Munn, Mihaela Rosca, David G. T. Barrett*  
- [Local Deep Implicit Functions for 3D Shape](https://arxiv.org/abs/1912.06126)  
  **[`CVPR 2020`]** *Kyle Genova, Forrester Cole, Avneesh Sud, Aaron Sarna, Thomas Funkhouser*  
- [CoCoNets: Continuous Contrastive 3D Scene Representations](https://arxiv.org/abs/2104.03851)  
  **[`arXiv 2021`]** *Shamit Lal, Mihir Prabhudesai, Ishita Mediratta, Adam W. Harley, Katerina Fragkiadaki* 
- [UWED: Unsigned Distance Field for Accurate 3D Scene Representation and Completion](https://arxiv.org/abs/2203.09167)  
  **[`arXiv 2022`]** *Jean Pierre Richa, Jean-Emmanuel Deschaud, François Goulette, Nicolas Dalmasso* 
- [The First Airborne Experiment of Sparse Microwave Imaging: Prototype System Design and Result Analysis](https://arxiv.org/abs/2110.10675)  
  **[`arXiv 2021`]**  *Zhe Zhang, Bingchen Zhang, Chenglong Jiang, Xingdong Liang, Longyong Chen, Wen Hong, Yirong Wu* 
- [Implicit Gradient Neural Networks with a Positive-Definite Mass Matrix for Online Linear Equations Solving](https://arxiv.org/abs/1703.05955)  
  **[`arXiv 2017`]** *Ke Chen* 
- [CoordX: Accelerating Implicit Neural Representation with a Split MLP Architecture](https://arxiv.org/abs/2201.12425)  
  **[`ICLR 2022`]** *Ruofan Liang, Hongyi Sun, Nandita Vijaykumar* 
- [In-Place Scene Labelling and Understanding with Implicit Scene Representation](https://arxiv.org/abs/2103.15875)  
**[`ICCV 2021`]** *Shuaifeng Zhi, Tristan Laidlow, Stefan Leutenegger, Andrew J. Davison*
- [Adversarial Generation of Continuous Images](https://arxiv.org/abs/2011.12026)  
**[`CVPR 2021`]** *Ivan Skorokhodov, Savva Ignatyev, Mohamed Elhoseiny*

- [Learning Implicit Fields for Generative Shape Modeling](https://arxiv.org/abs/1812.02822)  
  **[`CVPR 2019`]** *Zhiqin Chen, Hao Zhang*

- [GABO: Graph Augmentations with Bi-level Optimization](https://arxiv.org/abs/2104.00722)  
  **[`arXiv 2021`]** *Heejung W. Chung, Avoy Datta, Chris Waites*

- [Meta-Learning 3D Shape Segmentation Functions](https://arxiv.org/abs/2110.03854)  
  **[`arXiv 2021`]** *Yu Hao, Yi Fang*

- [Differentiable Volumetric Rendering: Learning Implicit 3D Representations without 3D Supervision](https://arxiv.org/abs/1912.07372)  
  **[`arXiv 2019`]** *Michael Niemeyer, Lars Mescheder, Michael Oechsle, Andreas Geiger*

- [BiCo-Net: Regress Globally, Match Locally for Robust 6D Pose Estimation](https://arxiv.org/abs/2205.03536)  
  **[`IJCAI 2022`]** *Zelin Xu, Yichen Zhang, Ke Chen, Kui Jia*

- [Scene Representation Networks: Continuous 3D-Structure-Aware Neural Scene Representations](https://arxiv.org/abs/1906.01618)  
  **[`arXiv 2019`]** *Vincent Sitzmann, Michael Zollhöfer, Gordon Wetzstein*

- [HybridPose: 6D Object Pose Estimation under Hybrid Representations](https://arxiv.org/abs/2001.01869)  
  **[`arXiv 2020`]** *Chen Song, Jiaru Song, Qixing Huang*

- [Multiview Neural Surface Reconstruction by Disentangling Geometry and Appearance](https://arxiv.org/abs/2003.09852)  
  **[`arXiv 2020`]** *Lior Yariv, Yoni Kasten, Dror Moran, Meirav Galun, Matan Atzmon, Ronen Basri, Yaron Lipman*

- [SOLO: A Simple Framework for Instance Segmentation ](https://arxiv.org/abs/2106.15947)  
  **[`arXiv 2021`]** *Xinlong Wang, Rufeng Zhang, Chunhua Shen, Tao Kong, Lei Li*





surface-based, volume-based

下面是用 implicit function + neural rendering 中隐式表征的通用形式：

$$
F_{\theta}:(\boldsymbol{p}, \boldsymbol{v}) \rightarrow (\boldsymbol{c}, \omega)
$$

where $\theta$ is parameters of an underlying neural network, $\boldsymbol{p}$ is the scene color, $\omega$ is the probility density (opacity) at spatial location $\boldsymbol{p}$, $\boldsymbol{v}$ is the ray direction. We can render a 2D image by shooting rays from a pin-hole camera position $\boldsymbol{p_0} \in \mathbb{R}^{3}$ to the 3D scene. The spatial location along the camera ray can be represented by $\boldsymbol{p}(z)=\boldsymbol{p}_{0}+z \cdot \boldsymbol{v}$. Note that $\omega$ is restricted only by $\boldsymbol{p}(z)$ while $\boldsymbol{c}$ is affected by both $\boldsymbol{p}$ and $\boldsymbol{v}$ to model view-dependent color. 

**surface rendering**

assume $\omega(\boldsymbol{p}(z))$ to be Dirac function $\delta(\boldsymbol{p}(z)-\boldsymbol{p}(z^{\*}))$ where $\boldsymbol{p}(z^{\*})$ is the intersection of the camera ray with the scene geometry.

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
