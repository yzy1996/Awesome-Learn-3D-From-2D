<h1 align="center">awesome 3D Diffusion</h1>

![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)
![PR's Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat)


A curated list of resources for Diffusion Models with 3D.

![图片 1](https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/202306241759169.png)



## Contributing

Feedback and contributions are welcome! If you think I have missed out on something (or) have any suggestions (papers, implementations and other resources), feel free to pull a request or leave an issue. I will release the [latex-pdf version]() in the future.  :arrow_down:markdown format:

``` markdown
[Paper Name](abs link)  
*[Author 1](homepage), Author 2, and Author 3*  
**[`Conference/Journal Year`] (`Institution`)** [[Code](link)] [[Project](link)]
```

:smile: Now you can use this [script](https://github.com/yzy1996/Python-Code/tree/master/Python%2BarXiv) to automatically generate the above text.



## Table of Contents

- [Introduction](#Introduction)
- [Literature](#Literature)
  - DM for Implicit
  - DM for Point Clouds
  - DM for Mesh



## Introduction

**这是一条将2D Diffusion Model迁移到3D生成的康庄大道**，2021年开始陆续出现了借助[GAN](https://github.com/yzy1996/Awesome-GANs)|[VAE](https://github.com/yzy1996/Awesome-Generative-Model/tree/main/1-Variational%20AutoEncoder%20(VAE)) 做 [3D-aware Generation](https://github.com/yzy1996/Awesome-Learn-3D-From-2D/tree/main/3D-Aware-Generation)，2022年[Diffusion Model](https://github.com/yzy1996/Awesome-Generative-Model/tree/main/2-Diffusion%20Model)开始席卷[2D Generation](https://github.com/yzy1996/Awesome-GANs)，那么一个很自然而然的想法就是[3D Diffusion](https://github.com/yzy1996/Awesome-Learn-3D-From-2D/tree/main/Diffusion%2B3D)。

谈及3D数据，那么一个绕不开的话题就是3D表征方式，主流的包括：voxels, point clouds, meshes, occupancy grids, radiance, etc. 第一个工作就是利用的点云表征，现在已经逐渐覆盖了所有表征范式。另一个突破点就是训练数据，这个和2D生成的发展类似（也就是如何利用最少的监督信息），早期的工作还是需要3D数据监督的，往后的发展肯定就是完全无监督的2D图像训练。

几个核心的技术点：

- Pure Diffusion Model (conditional and unconditional diffusion)
- Backbone Framework (2D U-Net -> 3D U-Net)
- 2D - 3D Representation and 3D-aware Generation

这个方向的目标是 **用2D图像数据训练生成高质量的3D形状 (generate high-fidelity 3D shape with 2D training data).**



还要考虑的几个问题 (Issues)：

- 内存占用。这是生成高质量结果带来的计算资源问题，一般可以拆分为 生成+超分辨率 两步来缓解，也可以利用混合表征形式 (hybrid explicit-implicit feature grid)。
- 表征结果样式。最终生成的形状用什么表示呢，continuous meshes 是比较好的选择，但其实主要想要的就是连续光滑且逼真，利用现有技术使得表征之间也是可以相互转化的。
- 3D一致性。这个只要构建的是 3D model 就行。



借助[参考2](https://zhuanlan.zhihu.com/p/592626748)，总结下3D表示+2D Diffusion做3D任务的四个流派：
- 用Diffusion优化3D隐式场（其中Diffusion可以是预训练的或者和3D隐式场联合训练的），特别是NeRF相关工作，例如DreamFusion和SparseFusion；Diffusion的作用是根据文本生成相应视角和内容的图片，事先使用2D生成模型拟合2D数据的多峰分布，再用其优化NeRF表示。用Diffusion优化NeRF，用Diffusion模型来重建NeRF看不到的细节，用NeRF来明确Diffusion模型对3D的感知。
- 使用3D Unet定制3D Diffusion，特别是point cloud相关工作；
- 把3D表示拆解并且重新拼接，变成超多通道2D图像，直接复用2D Diffusion，特别是Triplane相关工作，例如3D Neural Field Generation using Triplane Diffusion；
- 把2D Diffusion的Unet()换成一个renderer(encoder())的结构，即间接引入3D约束，例如RenderDiffusion；
  将3D约束编码成条件，用来约束2D Diffusion，例如DiffPose；



### 有哪些任务

- Reconstructing the 3D shape of an object from a single RGB image
- Unconditional shape generation or completion
- Sparse-view reconstruction
- 3D text-to-shape synthesis



### 输入的数据

- posed 2D image | unstructured 2D image

  > different views of the same object with known cameras, for example, obtained by means of structure from motion.
- image | video
- synthetic data | real-world data



## Literature

### DM for Implicit Re. (SDF, NeRF)

- [LION Latent Point Diffusion Models for 3D Shape Generation](http://arxiv.org/abs/2210.06978v1)  
  **[`NeurIPS 2022`]** *Xiaohui Zeng, Arash Vahdat, Francis Williams, Zan Gojcic, Or Litany, Sanja Fidler, Karsten Kreis*
- [IC3D Image-Conditioned 3D Diffusion for Shape Generation](http://arxiv.org/abs/2211.10865v2)  
  **[`arXiv 2022`]** *Cristian Sbrolli, Paolo Cudrano, Matteo Frosi, Matteo Matteucci*
- [Diffusion-SDF: Conditional Generative Modeling of Signed Distance Functions](https://arxiv.org/abs/2211.13757)  
  **[`arXiv 2022`]** *Gene Chou, Yuval Bahat, Felix Heide* 
- [Diffusion-based Image Translation using Disentangled Style and Content Representation](https://arxiv.org/abs/2209.15264)  
  **[`ICLR 2023`]** *Gihyun Kwon, Jong Chul Ye* 
- [Novel View Synthesis with Diffusion Models](https://arxiv.org/abs/2210.04628)  
  **[`ICLR 2023`]** *Daniel Watson, William Chan, Ricardo Martin-Brualla, Jonathan Ho, Andrea Tagliasacchi, Mohammad Norouzi* 
- [DreamFusion: Text-to-3D using 2D Diffusion](https://arxiv.org/abs/2209.14988)  
  **[`ICLR 2023`]** *Ben Poole, Ajay Jain, Jonathan T. Barron, Ben Mildenhall* 
- [SparseFusion Distilling View-conditioned Diffusion for 3D Reconstruction](http://arxiv.org/abs/2212.00792)  
  **[`CVPR 2023`]** *Zhizhuo Zhou, Shubham Tulsiani*
- [DiffRF: Rendering-Guided 3D Radiance Field Diffusion](https://arxiv.org/abs/2212.01206)  
  **[`CVPR 2023`]** *Norman Müller, Yawar Siddiqui, Lorenzo Porzi, Samuel Rota Bulò, Peter Kontschieder, Matthias Nießner* 
- [Diffusion-Based Signed Distance Fields for 3D Shape Generation](https://openaccess.thecvf.com/content/CVPR2023/papers/Shim_Diffusion-Based_Signed_Distance_Fields_for_3D_Shape_Generation_CVPR_2023_paper.pdf)  
  **[`CVPR 2023`]** *Jaehyeok Shim, Changwoo Kang and Kyungdon Joo*
- [3D Neural Field Generation using Triplane Diffusion](https://arxiv.org/abs/2211.16677)  
  **[`CVPR 2023`]** *J. Ryan Shue, Eric Ryan Chan, Ryan Po, Zachary Ankner, Jiajun Wu, Gordon Wetzstein* 
- [Latent-NeRF for Shape-Guided Generation of 3D Shapes and Textures](http://arxiv.org/abs/2211.07600v1)  
  **[`CVPR 2023`]** *Gal Metzer, Elad Richardson, Or Patashnik, Raja Giryes, Daniel Cohen-Or*
- [NeRDi: Single-View NeRF Synthesis with Language-Guided Diffusion as General Image Priors](https://arxiv.org/abs/2212.03267)  
  **[`CVPR 2023`]** *Congyue Deng, Chiyu "Max'' Jiang, Charles R. Qi, Xinchen Yan, Yin Zhou, Leonidas Guibas, Dragomir Anguelov* 
- [Diffusion-SDF Text-to-Shape via Voxelized Diffusion](http://arxiv.org/abs/2212.03293v2)  
  **[`CVPR 2023`]** *Muheng Li, Yueqi Duan, Jie Zhou, Jiwen Lu*
- [RenderDiffusion: Image Diffusion for 3D Reconstruction, Inpainting and Generation](https://arxiv.org/abs/2211.09869)  
  **[`CVPR 2023`]** *Titas Anciukevičius, Zexiang Xu, Matthew Fisher, Paul Henderson, Hakan Bilen, Niloy J. Mitra, Paul Guerrero* 
- [HOLODIFFUSION: Training a 3D Diffusion Model using 2D Images](https://arxiv.org/abs/2303.16509)  
  **[`CVPR 2023`]** *Animesh Karnewar, Andrea Vedaldi, David Novotny, Niloy Mitra* 
- [SDFusion Multimodal 3D Shape Completion Reconstruction and Generation](http://arxiv.org/abs/2212.04493v2)  
  **[`CVPR 2023`]** *Yen-Chi Cheng, Hsin-Ying Lee, Sergey Tulyakov, Alexander Schwing, Liangyan Gui*
- [HyperDiffusion: Generating Implicit Neural Fields with Weight-Space Diffusion](https://arxiv.org/abs/2303.17015)  
  **[`arXiv 2023`]** *Ziya Erkoç, Fangchang Ma, Qi Shan, Matthias Nießner, Angela Dai*


### DM for Point Clouds

<details><summary>Click to expand</summary>
<p>

> **Basic: Point Cloud Diffusion Models**

a diffusion model $\mathbb{R}^{3N} \mapsto \mathbb{R}^{3N}$ learn from a spherical ball into a recongnizable object.

</p>
</details>

- [3D Shape Generation and Completion through Point-Voxel Diffusion](https://arxiv.org/abs/2104.03670)  
  **[`ICCV 2021`]** *Linqi Zhou, Yilun Du, Jiajun Wu* 
- [Diffusion Probabilistic Models for 3D Point Cloud Generation](https://arxiv.org/abs/2103.01458)  
  **[`CVPR 2021`]** *Shitong Luo, Wei Hu* 
- [A Conditional Point Diffusion-Refinement Paradigm for 3D Point Cloud Completion](https://arxiv.org/abs/2112.03530)  
  **[`ICLR 2022`]** *Zhaoyang Lyu, Zhifeng Kong, Xudong Xu, Liang Pan, Dahua Lin* 
- [Point-E A System for Generating 3D Point Clouds from Complex Prompts](http://arxiv.org/abs/2212.08751v1)  
  **[`arXiv 2022`]** *Alex Nichol, Heewoo Jun, Prafulla Dhariwal, Pamela Mishkin, Mark Chen*
- [$PC^2$: Projection-Conditioned Point Cloud Diffusion for Single-Image 3D Reconstruction](https://arxiv.org/abs/2302.10668)  
  **[`CVPR 2023`]** *Luke Melas-Kyriazi, Christian Rupprecht, Andrea Vedaldi*


### DM for Mesh

- [MeshDiffusion Score-based Generative 3D Mesh Modeling](http://arxiv.org/abs/2303.08133v2)  
  **[`ICLR 2023`]** *Zhen Liu, Yao Feng, Michael J. Black, Derek Nowrouzezahrai, Liam Paull, Weiyang Liu*



## Related

https://github.com/yuchenlichuck/awesome-3D-Diffusion

https://zhuanlan.zhihu.com/p/592626748
