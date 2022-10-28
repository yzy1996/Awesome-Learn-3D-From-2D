# <p align=center>`Novel view Synthesis (NVS)` </p>

A collection of resources on Novel View Synthesis.

不管是用3D还是2D的方法，通过已有有限的视角数据，生成新视角的2D图片。最后的落脚点肯定是2D图片。

related project:

[visonpon/New-View-Synthesis](visonpon/New-View-Synthesis)

[paperswithcode/Novel View Synthesis](paperswithcode/Novel View Synthesis)



## Introduction

NVS techniques：可以先分成好几类

- explicitly reconstruction 

  只去构建表面

  然后这些方法无法生成高保真的结果

- volume-based representation 

相关工作有：Local Light Field Fusion， NeRF，Soft 3D Reconstruction for View Synthesis， SRN，Stereo Magnification: Learning View Synthesis using Multiplane Images

  model了整个空间，并且用volume rendering的方法生成图片

  这样带来的好处是：全局是连续的，都有了梯度，连续也可以高保真，

Neural Radiance Field (NeRF)



现存的一些方法是需要 每张图片的相机的参数，这个参数可以来自于

- 训练数据就有

- 通过一些技术估计 （例如 Structure-from-Motion）COLMAP

  



所以来了，怎么真正纯粹地只从RGB图像中生成呢？

- NeRF--





**The goal of novel view synthesis**: is to generate photo-realistic images of the same scene at novel viewpoints given a set (one or few) of posed images of a scene. A more challenging problem is NVS given just a single view. 

Recent promising research direction is to alongside neural scene representations.

To tackle the instability of the training procedure...



These methods can be divided into two categories:

- ...



View Synthesis: view interpolation

the goal is to interpolate views within the convex hull of the initial camera positions.



重点要关注的是 训练以及测试 的时候 需要哪些监督信号

![image-20220305161727758](https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/image-20220305161727758.png)



## Literature

[Multi-view to Novel View: Synthesizing Novel Views With Self-learned Confidence](https://openaccess.thecvf.com/content_ECCV_2018/papers/Shao-Hua_Sun_Multi-view_to_Novel_ECCV_2018_paper.pdf)  
**[`ECCV 2018`] (`USC, CMU`)**  
*Sun Shao-Hua, Huh Minyoung, Liao Yuan-Hong, Zhang Ning, Lim Joseph J*

[Space-time Neural Irradiance Fields for Free-Viewpoint Video](https://arxiv.org/abs/2011.12950)  
*Wenqi Xian, Jia-Bin Huang, Johannes Kopf, Changil Kim*  
**[`arXiv 2020`] (``)**

[Dynamic View Synthesis from Dynamic Monocular Video](https://arxiv.org/pdf/2105.06468.pdf)  
**[`Arxiv 2021`]  (`Virginia Tech, Facebook`)**  
*Chen Gao, Ayush Saraf, Johannes Kopf, Jia-Bin Huang*

[Dynamic View Synthesis from Dynamic Monocular Video](https://arxiv.org/abs/2105.06468)  
*Chen Gao, Ayush Saraf, Johannes Kopf, Jia-Bin Huang*  
**[`arXiv 2021`] (``)** 

[Generating Diverse Structure for Image Inpainting With Hierarchical VQ-VAE](https://arxiv.org/abs/2103.10022)  
*Jialun Peng, Dong Liu, Songcen Xu, Houqiang Li*  
**[`CVPR 2021`] (``)** 



[IBRNet: Learning Multi-View Image-Based Rendering](https://arxiv.org/abs/2102.13090)  
*Qianqian Wang, Zhicheng Wang, Kyle Genova, Pratul Srinivasan, Howard Zhou, Jonathan T. Barron, Ricardo Martin-Brualla, Noah Snavely, Thomas Funkhouser*  
**[`CVPR 2021`] (``)**

[Geometry-Free View Synthesis: Transformers and no 3D Priors](https://arxiv.org/abs/2104.07652)  
*Robin Rombach, Patrick Esser, Björn Ommer*  
**[`ICCV 2021`] (``)**
