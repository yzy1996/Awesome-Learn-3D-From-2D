# <p align=center>`Neural Radiance Fields`</p>

> 我们总希望机器能做到人能做到的事情，甚至要比人做得更好。



## Content

- Pose Estimation from RGB Images
  - [iNeRF](#iNeRF)
  - [NeRF--](#NeRF--)
  - [GNeRF](#GNeRF)




---

<span id="iNeRF"></span>
[iNeRF: Inverting Neural Radiance Fields for Pose Estimation](https://arxiv.org/pdf/2012.05877.pdf)  
**[`IROS 2021`] (`MIT, Google`)**  
*Lin Yen-Chen, Pete Florence, Jonathan T. Barron, Alberto Rodriguez, Phillip Isola, Tsung-Yi Lin*

<details><summary>Click to expand</summary><p>

<div align=center><img width="700" src="https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20210710160815.png"/></div>

> **Summary**

They propose to estimate [6 DoF pose]() of an image by inverting a NeRF model. They take three inputs: an observed image, an initial estimate of the pose, and a trained NeRF model.

The loss gradient is from the differences between the rendered image and the observed image. When they are aligned by repeated iteratively optimizing, yielding an accurate pose estimate.

> **Details**

Sampling strategy brings two orders of magnitude fewer pixels than a full-image sampling.

They assume that NeRF model $F_\Theta$ and the camera intrinsics are known, but the camera pose $T$ is undetermined. So the formulation can be written as:
$$
\hat{T}=\underset{T \in \operatorname{SE}(3)}{\operatorname{argmin}} \mathcal{L}(T \mid I, \Theta)
$$
To sample effectively, they propose to first employ interest point detector localizes the interest points and then apply a morphological dilation.

:x: 文中提到了一点是：他们这个方法可以用来让NeRF实现半监督学习，因为可以先用信息都已知的数据训练NeRF模型，然后增加一部分没有pose的图片，iNeRF输出pose，然后构成新的数据集继续训练NeRF。但这是半监督吗？（标准的半监督不是利用数据的结构信息去做分类，然后再增加部分标注信息，进而可以自动补全其他标注信息吗？）本身用不充分的信息，训练出了一个不充分的模型，用模型去做不充分预测，新的不充分数据继续训练这个不充分模型，结果依旧不充分，误差反而还可能累积了。

关于这个，作者也发现当标注信息过少时，效果反而还变差了。

> **Limitations**

- lighting and occlusion severely affect the performance.

- it needs a trained NeRF model which in turn requires known camera poses as supervision. (**硬伤啊！都训练好了再让你去估计相机位置，这是图啥？**) 

- slowly.

</p></details>

---

<span id="NeRF--"></span>
[NeRF--: Neural Radiance Fields Without Known Camera Parameters](https://arxiv.org/pdf/2102.07064.pdf)  
**[`Arxiv 2021`] (`Oxford`)** [[Code](https://github.com/ActiveVisionLab/nerfmm)]  
*Zirui Wang, Shangzhe Wu, Weidi Xie, Min Chen, Victor Adrian Prisacariu*

<details><summary>Click to expand</summary><p>

<div align=center><img width="700" src="https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20210713111427.png"/></div>

> **Summary**

They propose to jointly optimise the camera parameters for each input image while simultaneously training the NeRF model. 

> **Details**

They parameterize the camera rotation as: (skew matrix)
$$
\boldsymbol{R}=\boldsymbol{I}+\frac{\sin (\alpha)}{\alpha} \boldsymbol{\phi}^{\wedge}+\frac{1-\cos (\alpha)}{\alpha^{2}}\left(\boldsymbol{\phi}^{\wedge}\right)^{2}
\\
\boldsymbol{\phi}^{\wedge}=\left(\begin{array}{l}
\phi_{0} \\
\phi_{1} \\
\phi_{2}
\end{array}\right)^{\wedge}=\left(\begin{array}{ccc}
0 & -\phi_{2} & \phi_{1} \\
\phi_{2} & 0 & -\phi_{0} \\
-\phi_{1} & \phi_{0} & 0
\end{array}\right)
$$
To improve the quality of the synthesized images, after the first training process is completed, they drop the trained NeRF model and re-initialise it while keeping the trained camera parameters. Then they repeat the joint optimisation.

> **Limitation**

- struggles to reconstruct scenes with large texture-less regions or in the presence significant photometric inconsistency across frames.
- fall into local minima.
- roughly forward facing scenes and relatively short camera trajectories

</p></details>

---

<span id="GNeRF"></span>
[GNeRF: GAN-based Neural Radiance Field without Posed Camera](https://arxiv.org/pdf/2103.15606.pdf)  
**[`ICCV 2021`] (`ShanghaiTech`)**  
*Quan Meng, Anpei Chen, Haimin Luo, Minye Wu, Hao Su, Lan Xu, Xuming He, Jingyi Yu*

<details><summary>Click to expand</summary><p>

<div align=center><img width="700" src="https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20210709163102.png"/></div>

> **Summary**

They estimate both **camera poses** and **neural radiance fields** when the cameras are initialized at random poses in complex scenarios. Their algorithm has two phases: the first phase gets coarse camera poses and radiance fields with adversarial training; the second phase refines them jointly with a photometric loss.

> **Details**

看上图如果熟悉GAN的人肯定是很清楚对抗的过程，而Pose到生成再编码到Pose这样一个自监督的过程也很好理解。唯一的疑问是Pose Embedding是从哪里来的，难道是真样本自带的吗？

-> 不是数据集自带的！初始是随机采的，之后被优化更新。这里还要注意红色的Pose是固定的，不被更新，不是和真样本pair的。Pose的初始化对结果影响会很大，需要尽可能接近真实分布。



给定数据 $\mathcal{I} = \{I_1, I_2, \dots, I_n\}$，目标是得到对应的相机pose $\Phi = \{\phi_1, \phi_2, \dots, \phi_n\}$，有了pose就可以构建NeRF模型 $F_{\Theta}$ 了，用参数 $\Theta$ 表示。所以是为了优化得到准确的 $\Phi, \Theta$。
$$
\max _{\Theta} \min _{\eta} \mathcal{L}_{A}(\Theta, \eta) =\mathbb{E}_{I \sim P_{d}}[\log (D(I ; \eta))] +\mathbb{E}_{\hat{I} \sim P_{g}}[\log (1-D(\hat{I} ; \eta))]
\\
\min_{\theta_{E}} \mathcal{L}_{E}\left(\theta_{E}\right)=\mathbb{E}_{\phi \sim P(\phi)}\left[\left\|E\left(G\left(\phi ; F_{\Theta}\right) ; \theta_{E}\right)-\phi\right\|_{2}^{2}\right]
\\
\min \mathcal{L}_{R}(\Theta, \Phi)=\frac{1}{n} \sum_{i=1}^{n}\left\|I_{i}-G\left(\phi_{i} ; F_{\Theta}\right)\right\|_{2}^{2}+\frac{\lambda}{n} \sum_{i=1}^{n}\left\|E\left(I_{i} ; \theta_{E}\right)-\phi_{i}\right\|_{2}^{2}
$$
迭代更新法：先训练一次 G 和 D 来更新NeRF参数 $\Theta$ 和 参数 $\eta$，再训练一次 E 更新参数 $\theta_E$；初始化$\Phi$，固定 E，得到${\Phi}^{\prime}$，通过 loss 更新NeRF参数 $\Theta$ 和 $\Phi$。

不好理解的是 Phase A 那里的 Pose Embedding 是和什么对比训练的，其实是通过梯度下降优化的 Pose Embedding 和 Encoder 后出来的 Pose 对比。

> **Limitation**

- Require a reasonable camera pose sampling distribution not far from the true distribution.

- Not so accurate as of the COLMAP when there are sufficient information.

</p></details>

---





