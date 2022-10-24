# <p align=center>`Neural Radiance Fields`</p>

> 我们总希望机器能做到人能做到的事情，甚至要比人做得更好。





[GRAF](#GRAF)

[pi-GAN](#pi-GAN)

[GRF](#GRF)

[NeRF-Editing](#NeRF-Editing)

---

<span id="GRAF"></span>
[Generative Radiance Fields for 3D-Aware Image Synthesis](https://arxiv.org/pdf/2007.02442.pdf)  
**[`NeurIPS 2020`] (`MPI`) [[Code](https://github.com/autonomousvision/graf)]**  
*Katja Schwarz, Yiyi Liao, Michael Niemeyer, Andreas Geiger*

<details><summary>Click to expand</summary>


![image-20210108153435365](https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20210108153442.png)

> **Summary**



> **Details**

camera matrix $$\mathbf{K}$$

camera pose $$\mathbf{\xi}$$

2D sampling pattern $$\nu$$

shape code $$\mathbf{z}_s \in \mathbb{R}^m$$

appearance code $$\mathbf{z}_a \in \mathbb{R}^n$$


$$
\begin{aligned}
g_{\theta}: \mathbb{R}^{L_{\mathbf{x}}} \times \mathbb{R}^{L_{\mathbf{d}}} \times \mathbb{R}^{M_{s}} \times \mathbb{R}^{M_{a}} & \rightarrow \mathbb{R}^{+} \times \mathbb{R}^{3} \\
\left(\gamma(\mathbf{x}), \gamma(\mathbf{d}), \mathbf{z}_{s}, \mathbf{z}_{a}\right) & \mapsto(\sigma, \mathbf{c})
\end{aligned}
$$

</details>

---

<span id="pi-GAN"></span>
[Periodic Implicit Generative Adversarial Networks for 3D-Aware Image Synthesis](https://arxiv.org/pdf/2012.00926.pdf)  
**[`arxiv 2020`] (`Stanford`)**  
*Eric R. Chan, Marco Monteiro, Petr Kellnhofer, Jiajun Wu, Gordon Wetzstein*

<details><summary>Click to expand</summary>


> **Summary**

Synthesize high-quality view consistent images a SIREN-based 3D representation 

Using a method of combining sinusoidal representation networks and neural radiance fields.



multi-view consistency



> **Details**

First represent 3D object 



Density and color are defined as:
$$
\begin{align}
\sigma(\mathbf{x}) &=\mathbf{W}_{\sigma} \Phi(\mathbf{x})+\mathbf{b}_{\sigma}, \\
\mathbf{c}(\mathbf{x}, \mathbf{d}) &=\mathbf{W}_{c} \phi_{c}\left([\Phi(\mathbf{x}), \mathbf{d}]^{T}\right)+\mathbf{b}_{c},
\end{align}
$$


</details>

---

<span id="GRF"></span>
[GRF: Learning a General Radiance Field for 3D Scene Representation and Rendering](https://arxiv.org/pdf/2010.04595.pdf)  
**[`ICLR 2021`] (`Stanford`) [[Code](https://github.com/alextrevithick/GRF)]**  
*Alex Trevithick, Bo Yang*

<details><summary>Click to expand</summary>


> **Summary**



</details>

---

<span id="NeRF-Editing"></span>
[NeRF-Editing: Geometry Editing of Neural Radiance Fields](https://arxiv.org/abs/2205.04978)  
*Yu-Jie Yuan, Yang-Tian Sun, Yu-Kun Lai, Yuewen Ma, Rongfei Jia, Lin Gao*  
**[`CVPR 2022`] (`CAS`)**

<details><summary>Click to expand</summary>
<div align=center><img width="700" src="https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/image-20220512084132617.png"/></div>

> **Summary**

- Establish a correspondence between the extracted explicit mesh representation and the implicit neural representation of the target scene.
- Users first deform the mesh representation of the scene (well developed mesh-based deformation methods) and then bend the camera rays by introducing a tetragedra (四面体) mesh as a proxy.

> **Details**

- 

</details>

---

