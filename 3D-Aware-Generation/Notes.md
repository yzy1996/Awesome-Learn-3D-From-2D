# <p align=center>`3D Understanding`</p>

> 我们总希望机器能做到人能做到的事情，甚至要比人做得更好。



[RGBD-GAN](#RGBD-GAN)

[GRAM](#GRAM)

[liao2020unsupervised](#liao2020unsupervised)

---

<span id="RGBD-GAN"></span>
[RGBD-GAN: Unsupervised 3D Representation Learning From Natural Image Datasets via RGBD Image Synthesis](https://arxiv.org/pdf/1909.12573.pdf)  
*Atsuhiro Noguchi, Tatsuya Harada*  
**[`ICLR 2020`] (`U Tokyo, RIKEN`)**  

<details><summary>Click to expand</summary>

<div align=center><img width="500" src="https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20210709115756.png"/></div>

> **Summary**

They hope to understand **3D geometries** from 2D images by disentangling **object identity** (shape and texture) and **camera pose** (camera rotation, translation, and intrinsics). 

> **Details**

$T(x)$ donates a stochastic data augmentation function. $D(x)$ donates the last layer before the activation function. The proposed regularization is given by:

</details>

---

[Do 2D GANs Know 3D Shape? Unsupervised 3D shape reconstruction from 2D Image GANs](https://arxiv.org/pdf/2011.00844.pdf)  
*Xingang Pan, Bo Dai, Ziwei Liu, Chen Change Loy, Ping Luo*  
**[`ICLR 2021`] (`CUHK, NTU`)**

<details><summary>Click to expand</summary><p>



> **Summary**



</p></details>

---

[Image GANs meet Differentiable Rendering for Inverse Graphics and Interpretable 3D Neural Rendering](https://arxiv.org/pdf/2010.09125.pdf)  
*Yuxuan Zhang, Wenzheng Chen, Huan Ling, Jun Gao, Yinan Zhang, Antonio Torralba, Sanja Fidler*  
**[`ICLR 2021`] (`NVIDIA, Toronto`)**







### BlockGAN

[BlockGAN: Learning 3D Object-aware Scene Representations from Unlabelled Images](https://arxiv.org/pdf/2002.08988.pdf)  
*Thu Nguyen-Phuoc, Christian Richardt, Long Mai, Yong-Liang Yang, Niloy Mitra*  
**[`NeurIPS 2020`] (`University of Bath, Adobe`)** [[Code](https://github.com/thunguyenphuoc/BlockGAN)]

<details><summary>Click to expand</summary>

<div align=center><img width="600" src="https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20201214151442.png"/></div>

> **Summary**

learns 3D object-oriented scene representations directly from unlabeled 2D images

> **Method**

divide an 3D feature into background and foreground

a noise vector $\mathbb{z}_i$ and the object's 3D pose $\theta_i = (s_i, \mathbf{R}_i, \mathbf{t}_i)$

3D feature $O_i = g_i(\mathbb{z}_i, \theta_i)$
$$
\mathbf{x}=p\left(f(\underbrace{O_{0},}_{\text {background }} \underbrace{O_{1}, \ldots, O_{K}}_{\text {foreground }})\right)
$$

</details>

---

<span id="GRAM"></span>
[GRAM: Generative Radiance Manifolds for 3D-Aware Image Generation](https://arxiv.org/pdf/2112.08867.pdf)  
*Yu Deng, Jiaolong Yang, Jianfeng Xiang, Xin Tong*  
**[`arXiv 2021`] (`Tsinghua, Microsoft`)**



rather than Monte Carlo sampling

using a manifold predictor to predict a reduced space for point sampling and radiance field learning.



---

HoloGAN: Unsupervised Learning of 3D Representations From Natural Images

<details><summary>Click to expand</summary><p>
Main method:


> Traditional GANs learn to map a noise vector $z$ directly to 2D features to generate images.
>
> HoloGAN learn to map a learnt 3D representation to the 2D image space.

</p></details>



---

[Do 2D GANs Know 3D Shape? Unsupervised 3D shape reconstruction from 2D Image GANs](https://arxiv.org/pdf/2011.00844.pdf)  
*Xingang Pan, Bo Dai, Ziwei Liu, Chen Change Loy, Ping Luo*  
**[`ICLR 2021`] (`CUHK, NTU`)**  





[StyleSDF: High-Resolution 3D-Consistent Image and Geometry Generation](https://arxiv.org/abs/2112.11427)  
*Roy Or-El, Xuan Luo, Mengyi Shan, Eli Shechtman, Jeong Joon Park, Ira Kemelmacher-Shlizerman*  
**[`CVPR 2022`] (`U Washington`)** [Code](https://github.com/royorel/StyleSDF)

We usea coordinate-based MLP to model Signed Distance Fields (SDF) and radiance fields which render low resolution feature maps. 借助StyleGAN实现了高质量的生成，



输入采样的z 和 v，对于一条光线，volume renderer 会输出 每个采样点的 signed distance value + RGB + 256 feature vector。通过SDF的值，就能确定表面，同时将这些表面点对应的surface feature组合到一个featrue map。通过一个额外的2D generator将这个2D feature变成一个高清的图像 



已存在方法只完成了第一步，





<span id="liao2020unsupervised"></span>
[Towards Unsupervised Learning of Generative Models for 3D Controllable Image Synthesis](https://arxiv.org/pdf/1912.05237.pdf)  
**[`CVPR 2020`]** **(`MPI`)**  
*Yiyi Liao, Katja Schwarz, Lars Mescheder, Andreas Geiger*

<details><summary>Click to expand</summary><p>


> **Summary**

In this process, 3D supervision is hard to acquire,  



> **Details**

![image-20210428110836239](https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20210428110844.png)


$$
g_{\theta}^{3D}: \mathbf{z} \mapsto \{\mathbf{o}_{bg}, \mathbf{o}_1, \dots, \mathbf{o}_N\}
$$

$$
g_{\theta}^{2 D}: \mathbf{X}_{i}, \mathbf{A}_{i}, \mathbf{D}_{i} \mapsto \mathbf{X}_{i}^{\prime}, \mathbf{A}_{i}^{\prime}, \mathbf{D}_{i}^{\prime}
$$



Differentiable projection:

features map $\mathbf{X}_i \in \mathbb{R}^{W \times H \times F}$, initial alpha map $\mathbf{A}_i \in \mathbb{R}^{W \times H}$, initial depth map $\mathbf{D}_i \in \mathbb{R}^{W \times H}$.

> **Loss**

`Adversarial Loss` + `Compactness Loss` + `Geometric Consistency Loss`



</p></details>

--







[(VolumeGAN)3D-aware Image Synthesis via Learning Structural and Textural Representations](https://arxiv.org/abs/2112.10759)  
*Yinghao Xu, Sida Peng, Ceyuan Yang, Yujun Shen, Bolei Zhou*  
**[`CVPR 2022`] (`CUHK`)**


<details><summary>Click to expand</summary>

</p></details>

--





