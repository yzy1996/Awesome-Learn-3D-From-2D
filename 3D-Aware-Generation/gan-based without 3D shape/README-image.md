### CR-GAN

[CR-GAN: Learning Complete Representations for Multi-view Generation]()

**`[IJCAI 2018]`**	**`(Rutgers University)`**	**`[Yu Tian, Xi Peng]`**	**([:memo:]())**	**[[:octocat:](https://github.com/bluer555/CR-GAN)]**

<details><summary>Click to expand</summary><p>



<div align=center><img width="800" src="https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20201209160238.png" /></div>

> **Keywords**

Two-pathway



> Novelty

maintain the completeness of the learned embedding space.



> **Pipeline**

The generator $G$ produces a synthesis image $G(\mathbb{z}, v)$ with a random noise $\mathbb{z}$ under a view label $v$.

The discriminator $D$ contains two parts $(D_s, D_v)$. $D_s$ estimates the image quality, i.e., how real the image is, $D_v$ predict the view of given image.



The encoder $E$ reconstructs a latent vector $\bar{\mathbb{z}}$ from an image, in other words, $E$ will be learned as an inverse of $G$ and the latent space could represent the total image space.

In this problem, the output of $E$ should preserve the same identity and we hope $E$ could disentangle the viewpoint from the identity.

To be specific, we first sample a pair of real images $(\mathbb{x}_{i}, \mathbb{x}_{j})$ which are the same identity but different views $v_i,v_j$. The goal is to reconstruct $\mathbb{x}_j$ from $\mathbb{x}_i$. To achieve this, $E$ takes $\mathbb{x}_i$ as an input and outputs an identity-preserved representation $\bar{\mathbb{z}}$ together with the view estimation $\bar{\mathbb{v}}$: $(\bar{\mathbb{z}}, \bar{\mathbb{v}}) = E(\mathbb{x}_i)$. $G$ takes $\bar{\mathbb{z}}$ and $v_j$ as input, then produce $\tilde{\mathbb{x}}_{j}$ which should be the reconstruction of $\mathbb{x}_{j}$. 



在第一轮训练中，训练 $G$ 和 $D$， $G$ 想尽可能生成与真图像的假图，$D$ 想尽可能分辨出真图和假图。 

$\{D_s(\mathbb{x}), D_s(G(\mathbb{z}, v))\}$ 和 $\{D_v(\mathbb{x}), v\}$ 差距要尽可能小

> 只能同时识别身份和角度，建立的是真图和假图之间的关系，还缺乏同一身份不同角度真图或者假图之间的关系

在第二轮训练中，训练 $E$ 和 $D$，希望弥补上面的缺陷，$E$ 想尽可能解码出身份信息和角度信息，所以只要解开了，$G$ 就能继续生成，但 $D$ 需要重新训练别让把相同身份不同位置的



|                                                              |                                         |      |
| :----------------------------------------------------------: | :-------------------------------------: | :--: |
|                        $\mathbb{x}_i$                        | real image $\mathbb{x}$ with view $v_i$ |      |
|                        $\mathbb{x}_j$                        | real image $\mathbb{x}$ with view $v_j$ |      |
| $(\bar{\mathbb{z}}, \bar{\mathbb{v}}) = (E_{\mathbb{z}}(\mathbb{x}_i), E_v(\mathbb{x}_i))$ |                                         |      |
| $\tilde{\mathbb{x}}_{j} = G(E_\mathbb{z}(\mathbb{x}_{i}),v_j)$ |               fake image                |      |

- 



</p></details>

---

### DR-GAN

[Disentangled Representation Learning GAN for Pose-Invariant Face Recognition](https://openaccess.thecvf.com/content_cvpr_2017/papers/Tran_Disentangled_Representation_Learning_CVPR_2017_paper.pdf)

**`[CVPR 2017]`**	**`(MSU)`**	**`[Luan Tran, Xi Yin, Xiaoming Liu]`**	**([:memo:]())**	**[[:octocat:]()]**

<details><summary>Click to expand</summary><p>



![Generator-in-multi-image-DR-GAN-From-an-image-set-of-a-subject-we-can-fuse-the-features_W64](https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20200831160904.jpg)

![Comparison-of-previous-GAN-architectures-and-our-proposed-DR-GAN_W640](https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20200831161231.jpg)

**key words**: 

> Pose-Invariant Face Recognition (PIFR); 

**Problem:** 

> solve the problem of pose-invariant face recognition (PIFR), the goal is to extract the identity representation that is exclusive or invariant to pose and other variations.

**Related work:** 

> existing PIFR methods can be group into two categories - 1) employ face frontalization to synthesize a frontal face and then use traditional face recognition methods. 2) learn features directly from the non-frontal face.

**Impact:**

> help law enforcement practitioners identify suspects

**Main method:**

> - the input of $G_{enc}$ is **a face image** of any pose; the output is **a feature representation**.
> - the input of $G_{dec}$ is **a feature representation** above, **a pose code** $c$, and **a random noise vector** $z$; the output of $G_{dec}$ is **a synthetic face image** at a target pose
> - $D$ is trained to not only distinguish **real vs. fake** images, but also predict the **identity and pose** of a face.

**Mainly including three features:**

> - identity - represented by feature extracted by $G_{enc}$
> - pose - represented by pose code 
> - other facial feature (appearance variations) - represented by noise vector



The learning problem are twofold: 1) to learn a pose-invariant identity representation for PIFR, and 2) to synthesize a face image $\hat{x}$ with the same identity $y^d$ but a different pose specified by a pose code $c$.

The approach is to train a DR-GAN **conditioned** on the original image $x$ and the pose code $c$.



Given a face image with label $y = \{y^d, y^p\}$, where $y^d$ represents the label for identity and $y^p$ for pose. The discriminator $D = [D^d, D^p]$.

$\hat{x} = G(\mathbf{x}, c, z)$

</p></details>

---
