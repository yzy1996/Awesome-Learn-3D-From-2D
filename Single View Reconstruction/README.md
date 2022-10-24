# <p align=center>`Single View Reconstruction`</p>

**Single-view 3D Object Reconstruction is to recover 3D information, such as shape and texture, of the object from a single image.**



Impact: 3D scene analysis, robot navigation, and virtual/augmented reality



？这个话题 reconstruction 跟 synthesis 有很多区别吗？





Estimating object or scene geometery from only a single RGB image view 



很关键的一点是，如何从2D图像中学习3D信息，3D信息提取是来自这 category-specific 一类物体的，因此一定是 category level 的



所以这一笔记一定是和 Category-Specific 笔记密切相关的



## Introduction

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

















