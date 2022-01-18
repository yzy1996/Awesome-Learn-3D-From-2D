# <p align=center>`Single View Reconstruction`</p>



CMR needcameraparameter

UMR needsemanticparts





[ShapeHD](#ShapeHD)

[SMR](#smr)

---

<span id="ShapeHD"></span>
[Learning Shape Priors for Single-View 3D Completion and Reconstruction](https://arxiv.org/pdf/1809.05068.pdf)  
*Jiajun Wu, Chengkai Zhang, Xiuming Zhang, Zhoutong Zhang, William T. Freeman, Joshua B. Tenenbaum*  
**[`ECCV 2018`] (`MIT`)**  

<details><summary>Click to expand</summary><p>

<div align=center><img width="600" src="https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20210714105831.png"/></div>

> **Summary**

They just propose a penalty term to improve the quality of 3D reconstruction by integrating deep generative models with adversarially learned shape priors. After training the model, they can achieve single-view 3D shape completion and reconstruction.

> **Details**

Their model consists of three components:

- (encoder-decoder) 2.5D sketch estimator to predict the object's depth, surface normals, and silhouette from an RGB image.
- (encoder-decoder) 3D shape estimator to predict a 3D shape in the canonical view from 2.5D sketches.
- (discriminator from pre-trained GAN) deep naturalness model to penalize the shape estimator

</p></details>

---

[Self-Supervised 3D Mesh Reconstruction from Single Images](https://openaccess.thecvf.com/content/CVPR2021/html/Hu_Self-Supervised_3D_Mesh_Reconstruction_From_Single_Images_CVPR_2021_paper.html)  
*Tao Hu, Liwei Wang, Xiaogang Xu, Shu Liu, Jiaya Jia*    
**[`CVPR 2021`]**	**(`CUHK`)**  


<details><summary>Click to expand</summary><p>
3D attribute $A=[C, L, S, T]$, 3D object $O(S, T)$, where $C$ is Camera, $L$ is Light, $S$ is Shape, $T$ is Texture.

2D image $I$, its silhouette $M$

input $X=[I, M]$, 

their relations are:
$$
\text{rendering: } X = R(A)\\
\text{encoding: } A = E_\theta(X)
$$

<img src="https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20210410172628.png" alt="image-20210410172613853" style="zoom:50%;" />

</p></details>

---
