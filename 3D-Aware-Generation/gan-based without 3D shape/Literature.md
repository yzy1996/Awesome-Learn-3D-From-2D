[CR-GAN](#CR-GAN)



## CR-GAN

[CR-GAN: Learning Complete Representations for Multi-view Generation]()

**`[IJCAI 2018]`**	**`(Rutgers University)`**	**`[Yu Tian, Xi Peng]`**	**([:memo:]())**	**[[:octocat:](https://github.com/bluer555/CR-GAN)]**

<details><summary>Click to expand</summary><p>


</p></details>

---







---

**[`Disentangled Representation Learning GAN for Pose-Invariant Face Recognition`]**

**[`2017`]** **[`CVPR`]** **[[:octocat:](https://github.com/zhangjunh/DR-GAN-by-pytorch)]** 


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





**[`Defense-GAN: protecting classifiers against adversarial attacks using generative models`]**

**[`2018`]** **[`ICLR`]** **[[:memo:](./Defense-GAN.pdf)]** **[[:octocat:](https://github.com/kabkabm/defensegan)]**

<details><summary>Click to expand</summary><p>


**The main work:**

> To solve the problem of classification which is vulnerable to adversarial perturbations: carefully crafted small perturbations can cause misclassification of legitimate images. I can archive it into the field of **Machine deception**. (small perturbations do not affect human recognition but machine classifier)
>
> I can summarize their work as follows: given a picture with deception, GAN is used to generate the picture without deception, and finally classifier is used to classify.
>
> They use the GD of reconstruction error ($ \|G(\mathbf{z})-\mathbf{x}\|_{2}^{2} $) to find optimal $ G(z) $ 

**The methods it used:** 

- [ ] Several ways of attack: Fast Gradient Sign Method (FGSM), Randomized Fast Gradient Sign Method (RAND+FGSM), The Carlini-Wagner (CW) attack
- [ ] Lebesgue-measure

**Its contribution:**

> They proposed a novel defense strategy utilizing GANs to enhance the
> robustness of classification models against black-box and white-box adversarial attacks

**My Comments:**

> This work can be referred to using AE (Auto Encoder) for noise reduction. It’s just an easy application of GANs.
>

</p></details>

---

