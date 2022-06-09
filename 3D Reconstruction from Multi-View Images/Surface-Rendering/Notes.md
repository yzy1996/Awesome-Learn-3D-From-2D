# <p align=center>`[Title]`</p>

> The order is from the latest to the old



有关 Level set equation 的解释，$\phi(x(t), t) = 0$

https://profs.etsmtl.ca/hlombaert/levelset/



**celebrated dataset**

DTU MVS dataset





[CR-GAN](#CR-GAN)

---

<span id="CR-GAN"></span>
[Consistency regularization for generative adversarial networks](https://arxiv.org/pdf/1910.12027.pdf)  
**[ICLR 2020]  (`Google`)  [[Code](https://github.com/NVlabs/stylegan)]**  
*Tero Karras, Samuli Laine, Timo Aila*

<details><summary>Click to expand</summary><p>

> **Summary**

They propose a training stabilizer based on **consistency regularization**. In particular, they **augment data** passing into the GAN discriminator and **penalize the sensitivity** of the discriminator to these augmentations.

> **Details**

$T(x)$ donates a stochastic data augmentation function. $D(x)$ donates the last layer before the activation function. The proposed regularization is given by:

Latex
$$
\operatorname{argmin}_{\theta} \mathcal{L}(\theta)=\mathbb{E}_{\mathbf{z}, \mathbf{y}, \alpha}\left[\left(A\left(G\left(T_{\theta}(\mathbf{z}, \alpha), \mathbf{y}\right)\right)-(A(G(\mathbf{z}, \mathbf{y}))+\alpha)\right)^{2}\right]
$$

Latex2image
<div align=center><img src="https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20201119214216.svg"/></div>

figure
<div align=center><img width="300" src="https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20201119220419.png"/></div>

</p></details>

---



AtlasNet [18] learns an implicit representation that maps and assembles 2D squares
to 3D surface patches.





<span id="IDR"></span>
[Multiview Neural Surface Reconstruction by Disentangling Geometry and Appearance](https://arxiv.org/pdf/2003.09852.pdf)  
**[`NeurIPS 2020`] (`Weizmann Institute of Science`)**  
Lior Yariv, Yoni Kasten, Dror Moran, Meirav Galun, Matan Atzmon, Ronen Basri, Yaron Lipman

<details><summary>Click to expand</summary>
<div align="center"><img width="700" src="https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20210722165950.png" ></div>


> **Summary**



> **Details**

</details>

