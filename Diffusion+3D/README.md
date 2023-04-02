# 3D + Diffusion

Diffusion Probabilistic Models for 3D Point Cloud Generation

PC2: Projection-Conditioned Point Cloud Diffusion for Single-Image 3D Reconstruction





复制 2D-3D 生成任务的要点



 首先第一步就是 posed 2D image. 

> different views of the same object with known cameras, for example, obtained by means of structure from motion.



3D model: representation methods – a hybrid explicit-implicitfeature grid



3D 一致性 只要构建的是 3D model 就行

PC2: Projection-Conditioned Point Cloud Diffusion for Single-Image 3D Reconstruction





数据来源的问题，视频流



Diffsuion的作用是根据文本生成相应视角和内容的图片

事先使用2D生成模型拟合2D数据的多峰分布，再用其优化NeRF表示

用Diffusion优化NeRF，用Diffusion模型来重建NeRF看不到的细节，用NeRF来明确Diffusion模型对3D的感知。

调研了一阵子，稍微总结下3D表示+2D Diffusion做3D任务的四个流派：

用Diffusion优化3D隐式场（其中Diffusion可以是预训练的或者和3D隐式场联合训练的），特别是NeRF相关工作，例如DreamFusion和SparseFusion；
使用3D Unet定制3D Diffusion，特别是point cloud相关工作；
把3D表示拆解并且重新拼接，变成超多通道2D图像，直接复用2D Diffusion，特别是Triplane相关工作，例如3D Neural Field Generation using Triplane Diffusion；
把2D Diffusion的Unet()换成一个renderer(encoder())的结构，即间接引入3D约束，例如RenderDiffusion；
将3D约束编码成条件，用来约束2D Diffusion，例如DiffPose；





## 有哪些任务

- Reconstructing the 3D shape of an object from a singleRGB image
- unconditional shape generation or completion
- Sparse-view Reconstruction





## 输入的数据

- posed 2D image | unstructured 2D image
- image | video
- synthetic data | real-world data



## 几个直观的待解决的点

- 缺失的多视角信息怎么弥补：
  - 





## Literature

**Diffusion Models for Implicit Re. (SDF, NeRF)**

- [3D Neural Field Generation using Triplane Diffusion](https://arxiv.org/abs/2211.16677)  
  **[`arXiv 2022`]** *J. Ryan Shue, Eric Ryan Chan, Ryan Po, Zachary Ankner, Jiajun Wu, Gordon Wetzstein* 

- [DiffRF: Rendering-Guided 3D Radiance Field Diffusion](https://arxiv.org/abs/2212.01206)  
  **[`CVPR 2023`]** *Norman Müller, Yawar Siddiqui, Lorenzo Porzi, Samuel Rota Bulò, Peter Kontschieder, Matthias Nießner* 

- [Diffusion-based Image Translation using Disentangled Style and Content Representation](https://arxiv.org/abs/2209.15264)  
  **[`ICLR 2023`]** *Gihyun Kwon, Jong Chul Ye* 

- [Diffusion-SDF: Conditional Generative Modeling of Signed Distance Functions](https://arxiv.org/abs/2211.13757)  
  **[`arXiv 2022`]** *Gene Chou, Yuval Bahat, Felix Heide* 

- [DreamFusion: Text-to-3D using 2D Diffusion](https://arxiv.org/abs/2209.14988)  
  **[`ICLR 2023`]** *Ben Poole, Ajay Jain, Jonathan T. Barron, Ben Mildenhall* 

- [NeRDi: Single-View NeRF Synthesis with Language-Guided Diffusion as General Image Priors](https://arxiv.org/abs/2212.03267)  
  **[`CVPR 2023`]** *Congyue Deng, Chiyu "Max'' Jiang, Charles R. Qi, Xinchen Yan, Yin Zhou, Leonidas Guibas, Dragomir Anguelov* 

- [Novel View Synthesis with Diffusion Models](https://arxiv.org/abs/2210.04628)  
  **[`ICLR 2023`]** *Daniel Watson, William Chan, Ricardo Martin-Brualla, Jonathan Ho, Andrea Tagliasacchi, Mohammad Norouzi* 

- [RenderDiffusion: Image Diffusion for 3D Reconstruction, Inpainting and Generation](https://arxiv.org/abs/2211.09869)  
  **[`arXiv 2022`]** *Titas Anciukevičius, Zexiang Xu, Matthew Fisher, Paul Henderson, Hakan Bilen, Niloy J. Mitra, Paul Guerrero* 

- [HOLODIFFUSION: Training a 3D Diffusion Model using 2D Images](https://arxiv.org/abs/2303.16509)  
  **[`CVPR 2023`]** *Animesh Karnewar, Andrea Vedaldi, David Novotny, Niloy Mitra* 





**Diffusion Models for Point Clouds**

<details><summary>Click to expand</summary>
> **Basic: Point Cloud Diffusion Models**

a diffusion model $\mathbb{R}^{3N} \mapsto \mathbb{R}^{3N}$ learn from a spherical ball into a recongnizable object.

> **Details**

$T(x)$ donates a stochastic data augmentation function. $D(x)$ donates the last layer before the activation function. The proposed regularization is given by:

Latex
$$
\operatorname{argmin}_{\theta} \mathcal{L}(\theta)=\mathbb{E}_{\mathbf{z}, \mathbf{y}, \alpha}\left[\left(A\left(G\left(T_{\theta}(\mathbf{z}, \alpha), \mathbf{y}\right)\right)-(A(G(\mathbf{z}, \mathbf{y}))+\alpha)\right)^{2}\right]
$$

</details>

- [3D Shape Generation and Completion through Point-Voxel Diffusion](https://arxiv.org/abs/2104.03670)  
  **[`ICCV 2021`]** *Linqi Zhou, Yilun Du, Jiajun Wu* 

- [A Conditional Point Diffusion-Refinement Paradigm for 3D Point Cloud Completion](https://arxiv.org/abs/2112.03530)  
  **[`ICLR 2022`]** *Zhaoyang Lyu, Zhifeng Kong, Xudong Xu, Liang Pan, Dahua Lin* 

- [Diffusion Probabilistic Models for 3D Point Cloud Generation](https://arxiv.org/abs/2103.01458)  
  **[`CVPR 2021`]** *Shitong Luo, Wei Hu* 

- [$PC^2$: Projection-Conditioned Point Cloud Diffusion for Single-Image 3D Reconstruction](https://arxiv.org/abs/2302.10668)  
  **[`arXiv 2023`]** *Luke Melas-Kyriazi, Christian Rupprecht, Andrea Vedaldi*
