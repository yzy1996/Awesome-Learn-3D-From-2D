# <p align=center>`Neural Radiance Fields` </p>

> 这一个笔记主要围绕NeRF相关展开，通过相关文献，整理从为什么NeRF会诞生，到NeRF还存在的问题。
>
> 学nerf不得不看的几个链接
>
> https://dellaert.github.io/NeRF/
>
> https://paperswithcode.com/method/nerf
>
> https://github.com/vsitzmann/awesome-implicit-representations
>
> related link yenchen's [awesome-NeRF](https://github.com/yenchenlin/awesome-NeRF)



[NeRF: Representing Scenes as Neural Radiance Fields for View Synthesis](https://arxiv.org/pdf/2003.08934.pdf)  
**[`ECCV 2020`] (`UCB, UCSD`)**  
*Ben Mildenhall, Pratul P. Srinivasan, Matthew Tancik, Jonathan T. Barron, Ravi Ramamoorthi, Ren Ng*

<div align="center">
<img width=80% src="https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20201204115352.png"/>
    <p>Figure 1</p>
</div>
[Code-Tensorflow](https://github.com/bmild/nerf)  [Code-PyTorch](https://github.com/yenchenlin/nerf-pytorch)  [Code-PyTorch](https://github.com/krrish94/nerf-pytorch)

**In a nutshell / Short and sweet**: A Neural Radiance Field captures a volumetric representation of a specific scene within the weights of a neural network. NeRF represents the 3D geometry and appearance of a scene as a continuous 5D to 2D mapping function and uses volume rendering to synthesize novel views. The training process relies on multiple images with given camera poses.

## Introduction

因为能生成各种视角的图像，这样就能通过多视角的RGB图像构成重建Loss直接训练。



**The pipeline of NeRF**:

Let's assume that there is a 3D cubic space with an object in it. Any coordinate $(x,y,z)$​​​​ in this space can be queried whether it is occupied by the entity parts of this object. This occupancy is represented by 'volume density' $(\sigma)$​ in NeRF. Although the density in reality is a definite value of 0 or 1, it is expressed here as a probability. We also care about the color of this object specifically the surface. This color $(r,g,b)$​​​​ depends on the camera direction, so we need to query both the coordinate and the viewing direction $(\theta, \phi)$​​​. 

The above process can be formulated as a mapping function $f$ implemented by a neural network. A continuous function $f$ maps a 3D point $\mathbf{x} \in \mathbb{R}^3$ and a viewing direction $\mathbf{d} \in \mathbb{S}^2$ to a volume density $\sigma(\mathbf{x}) \in \mathbb{R}^+$ and an RGB color value $\mathbf{c}(\mathbf{x}, \mathbf{d}) \in \mathbb{R}^3$. 

<div align="center">
<img width=80% src="https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20210811231246.svg"/>
    <p>Figure 2</p>
</div>

After you figure out the main idea, you may naturally understand where the name-NeRF came from. **It can be seen as each point in the space emitting radiance in each direction**. The whole scene is like a radiance field (analogy with Magnetic Field).

The official description of this overall pipeline is:

> from a particular viewpoint, they 1) march camera rays through the scene to generate a sampled set of 3D points, 2) use those points and their corresponding 2D viewing directions as input to the neural network to produce an output set of colors and densities, and 3) use classical volume rendering techniques to accumulate those colors and densities into a 2D image. Because this process is naturally differentiable, we can use gradient descent to optimize this model by minimizing the error between each observed image and the corresponding views rendered from our representation. Minimizing this error across multiple views encourages the network to predict a coherent model of the scene by assigning high volume densities and accurate colors to the locations that contain the true underlying scene content.



**How to train the whole network:**

The training data is multiview images with known pose of an object. There are existing methods to render this 3D representation into a 2D image, so we can compare the difference between the reconstruction and the ground truth. Note that the whole process is differentiable.



**How to render:**

integrating the density and color at regular intervals along each viewing ray.

<div align="center"><img width="500" src="https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20210722155353.png" ></div>

$$
\begin{aligned}
\hat{C}(\mathbf{r}) &=\sum_{i=1}^{N} T_{i}\left(1-\exp \left(-\sigma_{\theta}\left(\mathbf{x}_{i}\right) \delta_{i}\right)\right) c_{\theta}\left(\mathbf{x}_{i}, \mathbf{d}\right) \\
T_{i} &=\exp \left(-\sum_{j<i} \sigma_{\theta}\left(\mathbf{x}_{j}\right) \delta_{j}\right)
\end{aligned}
$$

有多种采样方式

$p \in \mathbb{R}^3$



采样了点后再进行颜色融合（$\alpha$-composition ），



**Advantage of NeRF:**

- view-independent

Conditioning on the viewing direction $\mathbf{d}$ allows for modeling view-dependent effects such as specular reflections and improves reconstruction quality in case the Lambertian assumption is violated.

- no need of object's mask

While NeRF does not require object masks for training due to its volumetric radiance representation, extracting the scene geometry from the volume density requires careful tuning of the density threshold and leads to artifacts due to the ambiguity present in the density field.

- interpretability 可解释性



volume density does not admit accurate surface reconstruction

NeRF use volume rendering by learning alpha-compositing of a radiance field along rays.

high fidelity



**Disadvantage of NeRF:**

他的目的是做 novel-view synthesis，而不是 surface construction，只需要合成的照片正确就行，shape是否学的精确是不重要的，因为存在多解，找一个即可，而精确还原是只有一个解的。

对于NERF怎么找表面是通过一个 level-set，等水平面，因为已经学到了 density field

can only render novel views of a particular scene.





opacity value



我们可以作如下概括，

- 为何NeRF惊艳到了所有人
  - brutal simplicity (不讲道理地简单)，just an MLP taking in a 5D coordinate and outputting density and color

- 效果好的原因：
  - 神经网络强大，以及借助下面这些 tricks
  - periodic activation functions
  - positional encoding
  - stratified sampling scheme
- 存在的问题：
  - 训练和之后的渲染都很**慢**
  - 只能表征**静态**的场景
  - 依赖已知的**摄像头位置** (heavily rely on known camera pose)
  - 无法**泛化**到其他场景或目标 
  - 无法做到**少样本**训练 (fail to represent or synthesize with few instances)
  - 对**表面**的提取不够好

（后续的文献工作也主要是为了解决这些问题）



## Table of Contents

- [1. Improve Performance](#Improve-Performance)
- [2. Shape Encode](Shape-Encode)
- [3. Dynamic & Deformable](#Dynamic-&-Deformable)
- [4. Composition](Composition)
- [5. Pose Estimation](#Pose-Estimation)
- [6. Fast-Convergence](#Fast-Convergence)
- [7. Few-Samples](#Few-Samples)
- [8. Multiscale](#Multiscale)



### 1. Improve Performance

- [NeRF in the Wild: Neural Radiance Fields for Unconstrained Photo Collections](https://arxiv.org/pdf/2008.02268.pdf)  
  *Ricardo Martin-Brualla, Noha Radwan, Mehdi S. M. Sajjadi, Jonathan T. Barron, Alexey Dosovitskiy, Daniel Duckworth*  
  **[`CVPR 2021`]**

- [NeRF++: Analyzing and Improving Neural Radiance Fields](https://arxiv.org/pdf/2010.07492.pdf)  
  *Kai Zhang, Gernot Riegler, Noah Snavely, Vladlen Koltun*  
  **[`Arxiv 2020`] (`Cornell Tech, Intel`)** [[Code](https://github.com/Kai-46/nerfplusplus)]  

**data structures**

- [PlenOctrees for real-time rendering of neural radiance fields](https://arxiv.org/pdf/2103.14024.pdf)  
  *Alex Yu, Ruilong Li, Matthew Tancik, Hao Li, Ren Ng, Angjoo Kanazawa*  
  **[`Arxiv 2021`] (`UCB`)**  
  
- [Baking neural radiance fields for real-time view synthesis](https://arxiv.org/pdf/2103.14645.pdf)  
  *Peter Hedman, Pratul P. Srinivasan, Ben Mildenhall, Jonathan T. Barron, Paul Debevec*  
  **[`Arxiv 2021`] (`Google`)**  

**pruning**

- [Neural sparse voxel fields](https://arxiv.org/pdf/2007.11571.pdf)  
  *Lingjie Liu, Jiatao Gu, Kyaw Zaw Lin, Tat-Seng Chua, Christian Theobalt*  
  **[`NeurIPS 2020`] (`MPI`)**  

**importance sampling**

- [DONeRF: Towards Real-Time Rendering of Compact Neural Radiance Fields using Depth Oracle Networks](https://arxiv.org/pdf/2103.03231.pdf)  
  *Thomas Neff, Pascal Stadlbauer, Mathias Parger, Andreas Kurz, Joerg H. Mueller, Chakravarty R. Alla Chaitanya, Anton Kaplanyan, Markus Steinberger*  
  **[`EGSR 2021`] (`Graz University of Technology`)**  

**fast integration**

- [Autoint: Automatic integration for fast neural volume rendering](https://arxiv.org/pdf/2012.01714.pdf)  
  *David B. Lindell, Julien N. P. Martel, Gordon Wetzstein*  
  **[`CVPR 2021`] (`Stanford`)**  

**surface**



[CityNeRF: Building NeRF at City Scale](https://arxiv.org/pdf/2112.05504.pdf)  
*Yuanbo Xiangli, Linning Xu, Xingang Pan, Nanxuan Zhao, Anyi Rao, Christian Theobalt, Bo Dai, Dahua Lin*  
**[`arXiv 2021`]**



### 2. Shape/Texture Encode/Disentangle

> Including conditional nerf,  e.g. a single model to be used for multiple scenes.
>
> 同时encode的还有texture 或者叫 appearance，只是为了将他们解耦表征出来，然后做一点简单的替换就好了。

- [GRAF: Generative Radiance Fields for 3D-Aware Image Synthesis](https://arxiv.org/pdf/2007.02442.pdf)  
  *Katja Schwarz, Yiyi Liao, Michael Niemeyer, Andreas Geiger*  
  **[`NeurIPS 2020`] (`MPI`)** [[Code](https://github.com/autonomousvision/graf)]  

- [pi-GAN: Periodic Implicit Generative Adversarial Networks for 3D-Aware Image Synthesis](https://arxiv.org/pdf/2012.00926.pdf)  
  *Eric R. Chan, Marco Monteiro, Petr Kellnhofer, Jiajun Wu, Gordon Wetzstein*  
  **[`CVPR 2021`] (`Stanford`)**  

- [pixelNeRF: Neural Radiance Fields from One or Few Images](https://arxiv.org/pdf/2012.02190.pdf)  
  *Alex Yu, Vickie Ye, Matthew Tancik, Angjoo Kanazawa*  
  **[`CVPR 2021`] (`UCB`)**  

- [GRF: Learning a General Radiance Field for 3D Scene Representation and Rendering](https://arxiv.org/pdf/2010.04595.pdf)  
  *Alex Trevithick, Bo Yang*  
  **[`ICCV 2021`] (`Williams, Oxford, PolyU`)**  



### 3. Dynamic & Deformable

- [Nerfies: Deformable Neural Radiance Fields](https://arxiv.org/pdf/2011.12948.pdf)  
  *Keunhong Park, Utkarsh Sinha, Jonathan T. Barron, Sofien Bouaziz, Dan B Goldman, Steven M. Seitz, Ricardo Martin-Brualla*  
  **[`ICCV 2021`] (`Washington, Google`)** [[Code](https://github.com/google/nerfies)]  
- [Neural Scene Flow Fields for Space-Time View Synthesis of Dynamic Scenes](https://openaccess.thecvf.com/content/CVPR2021/papers/Li_Neural_Scene_Flow_Fields_for_Space-Time_View_Synthesis_of_Dynamic_CVPR_2021_paper.pdf)  
  *Zhengqi Li, Simon Niklaus, Noah Snavely, Oliver Wang*  
  **[`CVPR 2021`] (`Cornell`)**
- [D-NeRF: Neural Radiance Fields for Dynamic Scenes](https://arxiv.org/pdf/2011.13961.pdf)  
  *Albert Pumarola, Enric Corona, Gerard Pons-Moll, Francesc Moreno-Noguer*  
  **[`CVPR 2021`] (`CSIC-UPC, MPI`)**  
- [Dynamic Neural Radiance Fields for Monocular 4D Facial Avatar Reconstruction](https://arxiv.org/pdf/2012.03065.pdf)  
  *Guy Gafni, Justus Thies, Michael Zollhöfer, Matthias Nießner*  
  **[`CVPR 2021`] (`Technical University of Munich, Facebook`)**  
- [Neural Scene Graphs for Dynamic Scenes](https://arxiv.org/pdf/2011.10379.pdf)  
  *Julian Ost, Fahim Mannan, Nils Thuerey, Julian Knodt, Felix Heide*  
  **[`CVPR 2021`] (`Algolux, Technical University of Munich`)**  
- [Non-Rigid Neural Radiance Fields: Reconstruction and Novel View Synthesis of a Dynamic Scene From Monocular Video](https://arxiv.org/abs/2012.12247)  
  *Edgar Tretschk, Ayush Tewari, Vladislav Golyanik, Michael Zollhöfer, Christoph Lassner, Christian Theobalt*  
  **[`ICCV 2021`] (`MPI, Facebook`)** [[Code](https://github.com/facebookresearch/nonrigid_nerf)]  
- [HyperNeRF: A Higher-Dimensional Representation for Topologically Varying Neural Radiance Fields](https://arxiv.org/pdf/2106.13228.pdf)  
  *Keunhong Park, Utkarsh Sinha, Peter Hedman, Jonathan T. Barron, Sofien Bouaziz, Dan B Goldman, Ricardo Martin-Brualla, Steven M. Seitz*  
  **[`SIGGRAPH Asia 2021`] (`Washington, Google`)**



### Controllability & Edit

> compositional control of object location

- [Learning Object-Compositional Neural Radiance Field for Editable Scene Rendering](https://arxiv.org/pdf/2109.01847.pdf)  
  Bangbang Yang, Yinda Zhang, Yinghao Xu, Yijin Li, Han Zhou, Hujun Bao, Guofeng Zhang, Zhaopeng Cui  
  **[`ICCV 2021`] (`Zhejiang, Google, CUHK`)**

- [Unsupervised Discovery of Object Radiance Fields](https://arxiv.org/pdf/2107.07905.pdf)  
  *Hong-Xing Yu, Leonidas J. Guibas, Jiajun Wu*  
  **[`arXiv 2021`] (`Stanford`)**



> modifying the shape and appearance encoding, require a curated dataset of objects viewed
> under different views and colors

- [CodeNeRF: Disentangled Neural Radiance Fields for Object Categories](https://arxiv.org/pdf/2109.01750.pdf)  
  *Wonbong Jang, Lourdes Agapito*  
  **[`ICCV 2021`] (`UCL`)**

- [Editing Conditional Radiance Fields](https://arxiv.org/pdf/2105.06466.pdf)  
  *Steven Liu, Xiuming Zhang, Zhoutong Zhang, Richard Zhang, Jun-Yan Zhu, Bryan Russell*  
  **[`ICCV 2021`] (`MIT, Adobe`)**



- [FiG-NeRF: Figure-Ground Neural Radiance Fields for 3D Object Category Modelling](https://arxiv.org/pdf/2104.08418.pdf)  
  *Christopher Xie, Keunhong Park, Ricardo Martin-Brualla, Matthew Brown*  
  **[`arXiv 2021`] (`Washington, Google`)**

> edit material

- [NeRFactor: Neural Factorization of Shape and Reflectance Under an Unknown Illumination](https://arxiv.org/pdf/2106.01970.pdf)  
  Xiuming Zhang, Pratul P. Srinivasan, Boyang Deng, Paul Debevec, William T. Freeman, Jonathan T. Barron  
  **[`arXiv 2021`] (`MIT, Google`)**

- [CoNeRF: Controllable Neural Radiance Fields](https://arxiv.org/pdf/2112.01983.pdf)  
  Kacper Kania, Kwang Moo Yi, Marek Kowalski, Tomasz Trzciński, Andrea Tagliasacchi  
  [British Columbia, ]



### 4. Composition

- [GIRAFFE: Representing Scenes as Compositional Generative Neural Feature Fields](https://arxiv.org/pdf/2011.12100.pdf)  
  *Michael Niemeyer, Andreas Geiger*  
  **[`CVPR 2021`] (`MPI`)**   



### 5. Pose Estimation

Existing NeRF-based methods assume that the camera parameters are known. So it's better to train NeRF model without known camera poses. Even though there are some existing approaches (e.g. SfM) to pre-compute camera parameters.

也可以说解决的问题是，novel view synthesis from 2D images **without known camera poses**.

做到的效果包括：`一是有多准确`，`二是可变化范围有多大`

iNeRF and NeRF-- optimize camera pose along with other parameters when training NeRF.



- [iNeRF: Inverting Neural Radiance Fields for Pose Estimation](https://arxiv.org/pdf/2012.05877.pdf)  
  *Lin Yen-Chen, Pete Florence, Jonathan T. Barron, Alberto Rodriguez, Phillip Isola, Tsung-Yi Lin*  
  **[`IROS 2021`] (`MIT, Google`)**  

- [NeRF--: Neural Radiance Fields Without Known Camera Parameters](https://arxiv.org/pdf/2102.07064.pdf)  
  *Zirui Wang, Shangzhe Wu, Weidi Xie, Min Chen, Victor Adrian Prisacariu*  
  **[`Arxiv 2021`] (`Oxford`)** [[Code](https://github.com/ActiveVisionLab/nerfmm)]  

- [GNeRF: GAN-based Neural Radiance Field without Posed Camera](https://arxiv.org/pdf/2103.15606.pdf)  
  *Quan Meng, Anpei Chen, Haimin Luo, Minye Wu, Hao Su, Lan Xu, Xuming He, Jingyi Yu*  
  **[`Arxiv 2021`] (`ShanghaiTech`)**  

补充：其实谈到相机位置估计，不可避免会和 Structure-from-Motion (SfM) 去比较，他们的开源包叫COLMAP：

- [Structure-from-Motion Revisited](https://demuc.de/papers/schoenberger2016sfm.pdf)  
  *Johannes L. Schonberger, Jan-Michael Frahm*  
  **[`CVPR 2016`] (`UNC, ETH`)** [[Code](https://github.com/colmap/colmap)]  



### 6. Fast-Convergence

- [FastNeRF: High-Fidelity Neural Rendering at 200FPS](https://arxiv.org/abs/2103.10380)  
  *Stephan J. Garbin, Marek Kowalski, Matthew Johnson, Jamie Shotton, Julien Valentin*  
  **[`arXiv 2021`] (``)** 
- [KiloNeRF: Speeding up Neural Radiance Fields with Thousands of Tiny MLPs](https://arxiv.org/abs/2103.13744)  
  *Christian Reiser, Songyou Peng, Yiyi Liao, Andreas Geiger*  
  **[`ICCV 2021`] (``)** 
- [TensoRF: Tensorial Radiance Fields](https://arxiv.org/abs/2203.09517)  
  *Anpei Chen, Zexiang Xu, Andreas Geiger, Jingyi Yu, Hao Su*  
  **[`arXiv 2022`] (``)** 



### 7. Few-Samples

- [Putting NeRF on a Diet: Semantically Consistent Few-Shot View Synthesis](https://arxiv.org/abs/2104.00677)  
  *Ajay Jain, Matthew Tancik, Pieter Abbeel*  
  **[`ICCV 2021`] (``)**

- [InfoNeRF: Ray Entropy Minimization for Few-Shot Neural Volume Rendering]()  
  *Mijeong Kim, Seonguk Seo, Bohyung Han*  
  **[`CVPR 2022`]**

- [SinNeRF: Training Neural Radiance Fields on Complex Scenes from a Single Image](https://arxiv.org/abs/2204.00928)  
  *Dejia Xu, Yifan Jiang, Peihao Wang, Zhiwen Fan, Humphrey Shi, Zhangyang Wang*  
  **[`arXiv 2022`] (``)** 



### 8. Multiscale

- [Mip-NeRF: A Multiscale Representation for Anti-Aliasing Neural Radiance Fields](https://arxiv.org/pdf/2103.13415.pdf)  
  *Jonathan T. Barron, Ben Mildenhall, Matthew Tancik, Peter Hedman, Ricardo Martin-Brualla, Pratul P. Srinivasan*  
  **[`CVPR 2021`] (`Google`)**

- [Mip-NeRF 360: Unbounded Anti-Aliased Neural Radiance Fields](https://arxiv.org/pdf/2111.12077.pdf)  
  *Jonathan T. Barron, Ben Mildenhall, Dor Verbin, Pratul P. Srinivasan, Peter Hedman*  
  **[`arXiv 2021`] (`Google`)**



### Human

[A-NeRF: Articulated Neural Radiance Fields for Learning Human Shape, Appearance, and Pose](https://arxiv.org/pdf/2102.06199.pdf)  
*Shih-Yang Su, Frank Yu, Michael Zollhoefer, Helge Rhodin*  
**[`NeurIPS 2021`] (`British Columbia, Facebook`)**



## Trick

**(1) positional encoding**

Low dimensional input needs to be mapped to higher-dimensional features to be able to represent complex signals when $f$ is parameterized with a neural network. Specifically, we element-wise apply a pre-defined **positional encoding** to each component of $\mathbf{x}$ and $\mathbf{d}$.
$$
\gamma(t, L) = \left(\sin(2^0t\pi), \cos(2^0t\pi), \dots, \sin(2^{L}t\pi), \cos(2^{L}t\pi)\right),
$$
where $t$ is a scalar input, and $L$ the number of frequency octaves.

**(2) SIREN**



## Q&A

> Why not use a convolutional layer?

They are linear relation.



## Dataset

commonly-used single object datasets, Photoshape and image collections

- Chairs
- Cats
- CelebA
- CelebA-HQ

more challenging single-object

CompCars

LSUN Churches

FFHQ



Coordinate-based Image



To be sorted

Object-Centric Neural Scene Rendering





## Code

https://github.com/Jittor/JNeRF
