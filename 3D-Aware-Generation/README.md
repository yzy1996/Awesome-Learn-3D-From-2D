# <p align=center>`awesome 3D-aware Generation`</p>

[![Awesome](https://cdn.rawgit.com/sindresorhus/awesome/d7305f38d29fed78fa85652e3a63e154dd8e8829/media/badge.svg)](https://github.com/sindresorhus/awesome)
[![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)](https://GitHub.com/Naereen/StrapDown.js/graphs/commit-activity)
[![PR's Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat)](http://makeapullrequest.com) 

A collection of resources on 3D-aware generation or learning 3D from 2D, focusing on the thread of the methods utilizing neural implicit representation as an intermediate shape to achieve more strict 3D identity consistency (using 3D-aware features to represent a scene, and apply a neural renderer for realistic image synthesis). This collection is organized as follows:

- [Introduction](#Introduction)
- [Research Branch](#Research-Branch)
- [Literature](#Literature)



Ref rep: [awesome-3D-generation](https://github.com/justimyhxu/awesome-3D-generation)

### Contributing

Feedback and contributions are welcome! If you think I have missed out on something (or) have any suggestions (papers, implementations and other resources), feel free to pull a request or leave an issue. I will release the [latex-pdf version]() in the future.  :arrow_down:markdown format:

``` markdown
[Paper Name](abs link)  
*[Author 1](homepage), Author 2, and Author 3*  
**[`Conference/Journal Year`] (`Institution`)** [[Code](link)] [[Project](link)]
```

:exclamation: Now you can use this [script](https://github.com/yzy1996/Python-Code/tree/master/Python%2BarXiv) to automatically generate the above text.



## Introduction

<details><summary>中文介绍</summary>
<p>
**背景：**计算机视觉和图形学中的一大任务就是生成真实且可编辑的图像。过去几年，2D生成模型（GAN，VAE，Diffusion Model…）展示出了强大的能力，可以说已经很好地解决了这一难题。同时对3D生成的需求也在日益增强（现实世界就是3D的，3D信息带了更多应用），2D的载体是图像，3D的载体也应该是一种表征方式（Mesh, Grid Voxel, Point Cloud, Implicit…），在这里先笼统地称作3D表征。类比从2D数据集中学2D信息，从3D数据集中学3D信息变得理所当然，但3D数据集不像2D数据集那么多，且获取成本高，因此如何继续从2D数据集中挖掘潜在的3D信息就成为了关键。

**研究方向：**从上述背景介绍中就可以看出几条出路，1⃣️ 3D表征方式，哪种方式更好？表达能力强，速度快，代价低。2⃣️ 3D数据集有没有办法更容易制作呢？3⃣️ 如何从2D数据集中学？是从单物体多视角数据集（结构化的）学还是单物体单视角数据集（非结构化的）学？4⃣️ 生成的质量怎么样？是否能看出角度感，是否真实且高清。

**问题定义：**我们希望从2D数据集出发以实现任务。一方面我们想生成3D模型（可以360度旋转），另一方面3D模型 + 多个相机角度 = 多角度2D图像，前者可以被称为3D生成，后者可以被称为具有3D感知的图像生成（多视角图像生成）。多提一嘴，过拟合的方式是3D重建，泛化后是3D生成。

这里有一种特殊情况，就像2D生成一样，生成的对象结果由一个隐变量控制，这里也可以考虑用一个额外的隐变量控制角度，这种就没有生成3D模型。

我们最终想得到一个生成模型 $G$，给定一个隐变量 $z$ 和一个相机参数 $\theta$，生成一张图像，这两个变量都是可控的，前者决定生成的对象，后者决定生成的角度。3D模型 + 显式的相机参数就可以物理渲染出任意视角的2D图像，这样的效果会更好一些，相当于是先升维后再降维。
$$
G: (z \in \mathbb{R}^{d}, \theta \in \mathbb{R}^{3}) \mapsto I \in \mathbb{R}^{H \times W \times 3}
$$
**本文范畴：**其他会简略提及，主要是侧重通过无规则2D图像学3D隐式表征得到3Dshape然后给定相机参数渲染出任意角度的图像。



=如何得到3D模型 (3D mesh)

</p>
</details>



<details><summary>English Intro</summary>
<p>
Reconstructing 3D objects from 2D images is one of the mainstream problems in 3D computer vision. It is important for controlling the generation process to be able to manipulate some semantic attributes in the generated results. Among these attributes, 3D information such as pose has attracted much more attention.

**3D-aware image synthesis** aims to generate images of objects from multiple views by learning a 3D representation with explicit control over the camera pose. (generate 3D-consistent images with explicitly controllable camera poses.)

The key **challenge** is to do generate multi-view consistent and high-quality images.

performmulti-view joint optimization

Methods to solve can be categorized into two types: 1) learn a generator synthesise images under different disentangled feature; 2) learn a 3D shape representation as an intermediate process and cast images with differentiable rendering.

To ease the problem, researchers normally learn a 3D prior from a collection within a category, and also utilize some supervision signals, such as multiview images, pose labels, landmarks, and masks.

> **Problem settings:**

Given unstructured 2D image collections, 3D-aware image generation methods aim to learn a generative model that can explicitly control the camera viewpoint of the generated content. The generator G which takes a random noise $z$ and a camera pose $\theta$ as input, and outputs an image $I$ under pose $\theta$:

<div align=center><img width="300" src="https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/mylatex20220419_011353.svg"/></div>

**The goal is to** achieve parametric control and photo-realistic synthesis.

learning direct 3D representation of scenes and synthesize images under physical-based rendering process (volumetric rendering) to achieve more strict 3D consistency.

> difference between **multi-view generation from single image**

> **Training Strategy**

Using a non-saturating GAN loss with R1 regularization:

<div align=center><img width="600" src="https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/mylatex20220419_011253.svg"/></div>

add a pose regularization term:

<div align=center><img width="500" src="https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/mylatex20220419_011327.svg"/></div>

differentiable renderer allow one to infer 3D from 2D images without requiring 3D ground-truth 



existing volume rendering based methods suffer from the **resolution** and the **view-inconsistency** issues

</p>
</details>



> **Related subtitles**

- Pose-Disentangled 2D GANs
- Unsupervised 3D Reconstruction and Generationfrom 2D Images
- 3D prior for GANs



> **Future**

object-centric->large scale scene

object-centric->multi objects



## Literature

- [with 3D shape](#with-3D-shape)

  - [Implicit Representation](#Implicit-Representation)

  - [Voxel](#Voxel)

  - [Mesh](#Mesh)

  - [Hybrid](#Hybrid)

  - pre-defined 3D parameteric model

- [without 3D shape](#without-3D-shape)

  

### with-3D-shape

#### `Implicit Representation`

> For more information, plz ref [INR](https://github.com/yzy1996/Artificial-Intelligence/tree/main/1-Machine-Learning/1-Generative-Models/3D%20Representation%20%26%20Reconstruction/Neural%20Implicit%20Surfaces).

- [Unsupervised Learning of Probably Symmetric Deformable 3D Objects from Images in the Wild](https://arxiv.org/abs/1911.11130)  
  *Shangzhe Wu, Christian Rupprecht, Andrea Vedaldi*  
  **[`CVPR 2020 (Best paper)`]**  
- [GRAF: Generative Radiance Fields for 3D-Aware Image Synthesis](https://arxiv.org/abs/2007.02442)  
  *Katja Schwarz, Yiyi Liao, Michael Niemeyer, Andreas Geiger*  
  **[`NeurIPS 2020`] (`MPI`)** [[Code](https://github.com/autonomousvision/graf)]
- [NeRF-VAE: A Geometry Aware 3D Scene Generative Model](https://arxiv.org/abs/2104.00587)  
  *Adam R. Kosiorek, Heiko Strathmann, Daniel Zoran, Pol Moreno, Rosalia Schneider, Soňa Mokrá, Danilo J. Rezende*  
  **[`ICML 2021`] (`DeepMind`)**
- [GIRAFFE: Representing Scenes as Compositional Generative Neural Feature Fields](https://arxiv.org/abs/2011.12100)  
  *Michael Niemeyer, Andreas Geiger*  
  **[`CVPR 2021`] (`MPI`)** [[Code](https://github.com/autonomousvision/giraffe)]
- [pi-GAN: Periodic Implicit Generative Adversarial Networks for 3D-Aware Image Synthesis](https://arxiv.org/abs/2012.00926)  
  *Eric R. Chan, Marco Monteiro, Petr Kellnhofer, Jiajun Wu, Gordon Wetzstein*  
  **[`CVPR 2021`] (`Stanford`)**
- [Lifting 2D StyleGAN for 3D-Aware Face Generation](https://arxiv.org/abs/2011.13126)  
  *Yichun Shi, Divyansh Aggarwal, Anil K. Jain*  
  **[`CVPR 2021`] (`Michigan`)**
- [Unconstrained Scene Generation with Locally Conditioned Radiance Fields](https://arxiv.org/abs/2104.00670)  
  *Terrance DeVries, Miguel Angel Bautista, Nitish Srivastava, Graham W. Taylor, Joshua M. Susskind*  
  **[`ICCV 2021`] (`Apple`)**
- [A Shading-Guided Generative Implicit Model for Shape-Accurate 3D-Aware Image Synthesis](https://arxiv.org/abs/2110.15678)  
  *Xingang Pan, Xudong Xu, Chen Change Loy, Christian Theobalt, Bo Dai*  
  **[`NeurIPS 2021`] (`MPI, CUHK`)** [[Code](https://github.com/xingangpan/shadegan)]
- [Generative Occupancy Fields for 3D Surface-Aware Image Synthesis](https://arxiv.org/abs/2111.00969)  
  *Xudong Xu, Xingang Pan, Dahua Lin, Bo Dai*  
  **[`NeurIPS 2021`] (`CUHK, MPI`)** [[Code](https://github.com/SheldonTsui/GOF_NeurIPS2021)]
- [CIPS-3D: A 3D-Aware Generator of GANs Based on Conditionally-Independent Pixel Synthesis](https://arxiv.org/abs/2110.09788)  
  *Peng Zhou, Lingxi Xie, Bingbing Ni, Qi Tian*  
  **[`arXiv 2021`] [`SJTU`]** [[Code](https://github.com/PeterouZh/CIPS-3D)]
- [CAMPARI: Camera-Aware Decomposed Generative Neural Radiance Fields](https://arxiv.org/abs/2103.17269)  
  *Michael Niemeyer, Andreas Geiger*  
  **[`arXiv 2021`] (`MPI`)** [[Code](https://github.com/autonomousvision/campari)]
- [Do 2D GANs Know 3D Shape? Unsupervised 3D shape reconstruction from 2D Image GANs](https://arxiv.org/abs/2011.00844)  
  *Xingang Pan, Bo Dai, Ziwei Liu, Chen Change Loy, Ping Luo*  
  **[`ICLR 2021`] (`CUHK, NTU`)**  
- [StyleNeRF: A Style-based 3D-Aware Generator for High-resolution Image Synthesis](https://arxiv.org/abs/2110.08985)  
  *Jiatao Gu, Lingjie Liu, Peng Wang, Christian Theobalt*  
  **[`ICLR 2022`] (`Facebook, MPI`)** [[Code](https://github.com/facebookresearch/StyleNeRF)]
- [GRAM: Generative Radiance Manifolds for 3D-Aware Image Generation](https://arxiv.org/abs/2112.08867)  
  *Yu Deng, Jiaolong Yang, Jianfeng Xiang, Xin Tong*  
  **[`CVPR 2022`] (`Tsinghua, Microsoft`)**
- [StyleSDF: High-Resolution 3D-Consistent Image and Geometry Generation](https://arxiv.org/abs/2112.11427)  
  *Roy Or-El, Xuan Luo, Mengyi Shan, Eli Shechtman, Jeong Joon Park, Ira Kemelmacher-Shlizerman*  
  **[`CVPR 2022`] (`U Washington`)** 
- [Pix2NeRF: Unsupervised Conditional $π$-GAN for Single Image to Neural Radiance Fields Translation](https://arxiv.org/abs/2202.13162)  
  *Shengqu Cai, Anton Obukhov, Dengxin Dai, Luc Van Gool*  
  **[`CVPR 2022`] (`ETH`)**
- [GIRAFFE HD: A High-Resolution 3D-aware Generative Model](https://arxiv.org/abs/2203.14954)  
  *Yang Xue, Yuheng Li, Krishna Kumar Singh, Yong Jae Lee*  
  **[`CVPR 2022`] (`UCD`)**
- [Multi-View Consistent Generative Adversarial Networks for 3D-aware Image Synthesis](https://arxiv.org/abs/2204.06307)  
  *Xuanmeng Zhang, Zhedong Zheng, Daiheng Gao, Bang Zhang, Pan Pan, Yi Yang*  
  **[`CVPR 2022`] (`University of Technology Sydney`)**
- [VoLux-GAN: A Generative Model for 3D Face Synthesis with HDRI Relighting](https://arxiv.org/abs/2201.04873)  
  *Feitong Tan, Sean Fanello, Abhimitra Meka, Sergio Orts-Escolano, Danhang Tang, Rohit Pandey, Jonathan Taylor, Ping Tan, Yinda Zhang*  
  **[`arXiv 2022`] (`Google`)** 
- [3D-GIF: 3D-Controllable Object Generation via Implicit Factorized Representations](https://arxiv.org/abs/2203.06457)  
  *Minsoo Lee, Chaeyeon Chung, Hojun Cho, Minjung Kim, Sanghun Jung, Jaegul Choo, Minhyuk Sung*  
  **[`arXiv 2022`] (`KAIST`)** 
- [GRAM-HD: 3D-Consistent Image Generation at High Resolution with Generative Radiance Manifolds](https://arxiv.org/abs/2206.07255)  
  *Jianfeng Xiang, Jiaolong Yang, Yu Deng, Xin Tong*  
  **[`arXiv 2022`] (``)** 



#### `Voxel`

- [HoloGAN: Unsupervised learning of 3D representations from natural images](https://arxiv.org/abs/1904.01326)  
  *Thu Nguyen-Phuoc, Chuan Li, Lucas Theis, Christian Richardt, Yong-Liang Yang*  
  **[`ICCV 2019`] (`University of Bath`)**

- [BlockGAN: Learning 3D Object-aware Scene Representations from Unlabelled Images](https://arxiv.org/abs/2002.08988)  
  *Thu Nguyen-Phuoc, Christian Richardt, Long Mai, Yong-Liang Yang, Niloy Mitra*  
  **[`NeurIPS 2020`] (`University of Bath, Adobe`)**



#### `Mesh`

- [Unsupervised Generative 3D Shape Learning from Natural Images](https://arxiv.org/abs/1910.00287)  
  *Attila Szabó, Givi Meishvili, Paolo Favaro*  
  **[`arXiv 2019`] (`Bern`)**

- [Image GANs meet Differentiable Rendering for Inverse Graphics and Interpretable 3D Neural Rendering](https://arxiv.org/abs/2010.09125)  
  *Yuxuan Zhang, Wenzheng Chen, Huan Ling, Jun Gao, Yinan Zhang, Antonio Torralba, Sanja Fidler*  
  **[`ICLR 2021`] (`NVIDIA, U Toronto`)**  
  
- [Leveraging 2D Data to Learn Textured 3D Mesh Generation](https://arxiv.org/abs/2004.04180)  
  *Paul Henderson, Vagia Tsiminaki, Christoph H. Lampert*  
  **[`CVPR 2020`]** ()



#### `Depth`

- [RGBD-GAN: Unsupervised 3D Representation Learning From Natural Image Datasets via RGBD Image Synthesis](https://arxiv.org/abs/1909.12573)  
  *Atsuhiro Noguchi, Tatsuya Harada*  
  **[`ICLR 2020`] (`U Tokyo, RIKEN`)**  

- [3D-Aware Indoor Scene Synthesis with Depth Priors](https://arXiv.org/abs/2202.08553)  
  *Zifan Shi, Yujun Shen, Jiapeng Zhu, Dit-Yan Yeung, Qifeng Chen*  
  **[`arXiv 2022`] (`HKUST`)**  [Code](https://github.com/VivianSZF/depthgan) [Project Page](https://vivianszf.github.io/depthgan/)



#### `Hybrid`

- [3D-aware Image Synthesis via Learning Structural and Textural Representations](https://arxiv.org/abs/2112.10759)  
  *Yinghao Xu, Sida Peng, Ceyuan Yang, Yujun Shen, Bolei Zhou*  
  **[`CVPR 2021`] (`CUHK`)** [[Code](https://github.com/genforce/volumegan)]

- [Efficient Geometry-aware 3D Generative Adversarial Networks](https://arxiv.org/abs/2112.07945)  
  *Eric R. Chan, Connor Z. Lin, Matthew A. Chan, Koki Nagano, Boxiao Pan, Shalini De Mello, Orazio Gallo, Leonidas Guibas, Jonathan Tremblay, Sameh Khamis, Tero Karras, Gordon Wetzstein*  
  **[`CVPR 2021`] (`Stanford`)** [[Code](https://github.com/NVlabs/eg3d)]



#### `pre-defined model`

> see [related](#related)

- [GIF: Generative Interpretable Faces](https://arxiv.org/abs/2009.00149)  
  *Partha Ghosh, Pravir Singh Gupta, Roy Uziel, Anurag Ranjan, Michael Black, Timo Bolkart*  
  **[`3DV 2020`] (`MPI`)** [[Code](https://github.com/ParthaEth/GIF)]



### without 3D shape

> just for background comparison.





## Related

predefined 3D face model

- [FLAME](https://flame.is.tue.mpg.de/)
- [3DMM]()



[3D Shape Induction from 2D Views of Multiple Objects](https://arxiv.org/abs/1612.05872)  
*Matheus Gadelha, Subhransu Maji, Rui Wang*  
**[`CVPR 2017`] (``)** 

[Unsupervised Learning of 3D Structure from Images](https://arxiv.org/abs/1607.00662)  
*Danilo Jimenez Rezende, S. M. Ali Eslami, Shakir Mohamed, Peter Battaglia, Max Jaderberg, Nicolas Heess*  
**[`NeurIPS 2016`] (``)**

[Inverse Graphics GAN: Learning to Generate 3D Shapes from Unstructured 2D Data](https://arxiv.org/abs/2002.12674)  
*Sebastian Lunz, Yingzhen Li, Andrew Fitzgibbon, Nate Kushman*  
**[`arXiv 2020`] (``)** 







