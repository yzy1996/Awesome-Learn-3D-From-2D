<h1 align="center">awesome 3D Diffusion</h1>

<div align="center">
![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)
![PR's Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat)
</div>

A curated list of resources for Diffusion Models with 3D.



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
- [Literature](Literature)
  - DM for Implicit
  - DM for Point Clouds
  - DM for Mesh



## Introduction

这是一个直接将2D Diffusion Model迁移到3D生成的直接想法。最早的结合是和Point clouds（PointNet），然后发展到隐式表征。首先要很清晰Diffusion Model的原理，迁移到3D的主要改变是将2D U-Net 变成 3D U-Net。

生成要是可以condition类别的，

SDF 可以看成是 point cloud 的改进版，

- conditional and unconditional diffusion 
- 2D - 3D Representation 
- 3D-aware Generation



这个方向的目的是 **generate high-fidelity 3D shape**



**Memory Issues**：要生成高质量的结果就会存在这个问题，那么可以拆分为 生成+超分辨率 两步来做。



continuous surfaces of 3D shapes

reconstruct continuous meshes from point clouds





3D model: representation methods – a hybrid explicit-implicit feature grid



Diffusion的作用是根据文本生成相应视角和内容的图片

事先使用2D生成模型拟合2D数据的多峰分布，再用其优化NeRF表示

用Diffusion优化NeRF，用Diffusion模型来重建NeRF看不到的细节，用NeRF来明确Diffusion模型对3D的感知。

调研了一阵子，稍微总结下3D表示+2D Diffusion做3D任务的四个流派：

用Diffusion优化3D隐式场（其中Diffusion可以是预训练的或者和3D隐式场联合训练的），特别是NeRF相关工作，例如DreamFusion和SparseFusion；

- 使用3D Unet定制3D Diffusion，特别是point cloud相关工作；
- 把3D表示拆解并且重新拼接，变成超多通道2D图像，直接复用2D Diffusion，特别是Triplane相关工作，例如3D Neural Field Generation using Triplane Diffusion；
- 把2D Diffusion的Unet()换成一个renderer(encoder())的结构，即间接引入3D约束，例如RenderDiffusion；
  将3D约束编码成条件，用来约束2D Diffusion，例如DiffPose；



## 有哪些任务

- Reconstructing the 3D shape of an object from a singleRGB image
- unconditional shape generation or completion
- Sparse-view Reconstruction

text-to-shape synthesis





## 输入的数据

- posed 2D image | unstructured 2D image

  > different views of the same object with known cameras, for example, obtained by means of structure from motion.
- image | video
- synthetic data | real-world data



## 几个直观的待解决的点

- 缺失的多视角信息怎么弥补：
  - .
- 3D 一致性 只要构建的是 3D model 就行



主要看Diffusion在里面起到的作用，和怎么实现的



voxel grid 和 pixel 直接类比，将 2D Unet 直接迁移到 3D-Unet

<img src="https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/202306081048497.png" alt="image-20230608104129451" style="zoom:50%;" />



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

> **Details**

$T(x)$ donates a stochastic data augmentation function. $D(x)$ donates the last layer before the activation function. The proposed regularization is given by:

$$
\operatorname{argmin}_{\theta} \mathcal{L}(\theta)=\mathbb{E}_{\mathbf{z}, \mathbf{y}, \alpha}\left[\left(A\left(G\left(T_{\theta}(\mathbf{z}, \alpha), \mathbf{y}\right)\right)-(A(G(\mathbf{z}, \mathbf{y}))+\alpha)\right)^{2}\right]
$$

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




## Related Project

https://github.com/yuchenlichuck/awesome-3D-Diffusion

https://zhuanlan.zhihu.com/p/592626748
