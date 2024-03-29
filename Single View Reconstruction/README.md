# <p align=center>`Single View Reconstruction`</p>

**Single-view 3D Object Reconstruction is to recover 3D information, such as shape and texture, of the object from a single image.**



从单张图像重建整个3D场景是很重要的一个话题，more details see [file](./Single-View-Reconstruction)

也可以叫 single image reconstruction，对一个 3D 目标，单个图像就是单个视角



Impact: 3D scene analysis, robot navigation, and virtual/augmented reality



？这个话题 reconstruction 跟 synthesis 有很多区别吗？





Estimating object or scene geometery from only a single RGB image view 



很关键的一点是，如何从2D图像中学习3D信息，3D信息提取是来自这 category-specific 一类物体的，因此一定是 category level 的



所以这一笔记一定是和 Category-Specific 笔记密切相关的



## Introduction

划分为：3D supervised| 2D supervised | unsupervised 



3D attributes, including camera, shape, texture, and light



重建什么？object's shape and texture

只需要一张图片吗？不，还需要2D image-level annotation

方法的发展进步：

- fit the parameters of a 3D prior morphable model (3DMM)

> building these prior models is expensive and time-consuming

- deep model 3D supervised reconstruction

> 需要3D ground truth, attributes or annotation

- 2D supervised reconstruction

> key modules is a differentiable render 





更多的是指训练好的模型具有这个能力，而训练过程是通过多视角图像的





主要的方法有：

- fit the parameters of a 3D prior morphable model, such as 3DMM for faces and SMPL for human,





Interpolated Consistency

landmark consistency





## Literature

<span id="ShapeHD"></span>
[Learning Shape Priors for Single-View 3D Completion and Reconstruction](https://arxiv.org/pdf/1809.05068.pdf)  
*Jiajun Wu, Chengkai Zhang, Xiuming Zhang, Zhoutong Zhang, William T. Freeman, Joshua B. Tenenbaum*  
**[`ECCV 2018`] (`MIT`)**

<span id="CMR"></span>
[Learning Category-Specific Mesh Reconstruction from Image Collections](https://arxiv.org/pdf/1803.07549.pdf)  
*Angjoo Kanazawa, Shubham Tulsiani, Alexei A. Efros, Jitendra Malik*  
**[`ECCV 2018`] (`UCB`)** [[Code](https://github.com/akanazawa/cmr)]

<span id="UMR"></span>
[Self-supervised Single-view 3D Reconstruction via Semantic Consistency](https://arxiv.org/pdf/2003.06473.pdf)  
*Xueting Li, Sifei Liu, Kihwan Kim, Shalini De Mello, Varun Jampani, Ming-Hsuan Yang, Jan Kautz*  
**[`ECCV 2020`] (`NVIDIA`)** [[Code](https://github.com/NVlabs/UMR)]

<span id="UnsupD"></span>
[Unsupervised Learning of Probably Symmetric Deformable 3D Objects from Images in the Wild](https://arxiv.org/pdf/1911.11130.pdf)  
*Shangzhe Wu, Christian Rupprecht, Andrea Vedaldi*  
**[`CVPR 2020`]  (`Oxford`)**

<span id="SMR"></span>
[Self-Supervised 3D Mesh Reconstruction from Single Images](https://openaccess.thecvf.com/content/CVPR2021/html/Hu_Self-Supervised_3D_Mesh_Reconstruction_From_Single_Images_CVPR_2021_paper.html)  
*Tao Hu, Liwei Wang, Xiaogang Xu, Shu Liu, Jiaya Jia*    
**[`CVPR 2021`]**	**(`CUHK`)**

[CoReNet: Coherent 3D scene reconstruction from a single RGB image](https://arxiv.org/abs/2004.12989)  
*Stefan Popov, Pablo Bauszat, Vittorio Ferrari*  
**[`ECCV 2020`] ()**

[3D Scene Reconstruction from a Single Viewport](https://www.ecva.net/papers/eccv_2020/papers_ECCV/papers/123670052.pdf)  
*Maximilian Denninger, Rudolph Triebel*  
**[`ECCV 2020`] (`DLR, TUM`)**

[Panoptic 3D Scene Reconstruction From a Single RGB Image](https://arxiv.org/pdf/2111.02444.pdf)  
*Manuel Dahnert, Ji Hou, Matthias Nießner, Angela Dai*  
**[`NeurIPS 2021`] (`TUM`)**

Deep 3D Portrait from a Single Image

[3D Scene Reconstruction with Multi-layer Depth and Epipolar Transformers]()  
*Daeyun Shin, Zhile Ren, Erik B. Sudderth, Charless C. Fowlkes*  
**[`ICCV 2019`] (`UCI, Georgia`)**





本质工作是重建3D形状，但方法主要有几种：

一种是从多视角图像中学习，因为多个视角可以具备

还有一种是如果不从多视角，可以少一些样本，但

还有一种是单样本，那么就需要同类型的多种，因为同类型是有共性的，因此也是可以学到一定的偏置归纳



伴随着这些基本任务，也有预测相机姿态和深度，



而有了3D shape，再生成新视角就比较容易了。



需要思考的一个点是为什么很多工作只侧重一点，看起来很多任务都可以协同完成，包括新视角的生成。

所以为了解答这个疑惑，我重新阅读了相关论文。

- 新视角生成：有没有先重建3D形状呢。
- 相机视角和深度估计：有了3d形状，是不是只要你加上摄像机位置，就能很容易估计深度，



所以底层的核心是，用什么样的表征方式，以及怎样去学。（整个过程是否是可导的，对数据学习约束的要求）



3D-aware representation 

3D reconstruction

3D generation



是额外的步骤在学习吗









这里面就需要涉及

- 基础工作是 从2D单张图直接重建3D形状

- 是否有带相关性（多彩颜色），其实是个附属
- 

| 论文名 | 数据集 | 是否需要3D | 是否需要相机视角 | 是否需要轮廓图 |
| :----: | :----: | :--------: | :--------------: | :------------: |
|  TARS  |        |            |                  |                |
|        |  人脸  |            |                  |                |
|        |        |            |                  |                |







