### Reconstruction error

- pSNR

$$
\operatorname{pSNR}(I, R)=-20 \log _{10} \frac{\operatorname{MAX}(I)}{\sqrt{\operatorname{MSE}(I, R)}}
$$

where MAX corresponds to the maximal value the image I can attain, and MSE is the Mean Squared Error.

- Patch-Wise Minimal Pixels

Let an image $I \in \mathbb{R}^{m \times n \times c}$ be divided into $P$ non-overlapped patches with a patch size of $r \times r$, for with $P=\left\lceil\frac{m}{r}\right\rceil \cdot\left[\frac{n}{r}\right]$.
$$
\mathcal{P}(I)(i)=\min _{(x, y) \in \Omega_{i}}\left(\min _{c \in\{r, g, b\}} I(x, y, c)\right)
$$

- For 3D Point Clouds

There are two setpoints clouds A and B, and we hope to use some useful metrics to measure the accurancy.

- JSD (Jensen-Shannon Divergence)
  $$
  J S D\left(P_{A} \| P_{B}\right)=\frac{1}{2} D\left(P_{A} \| M\right)+\frac{1}{2} D\left(P_{B} \| M\right)
  $$
  where $M = \frac{1}{2} (P_A + P_B)$



[github](https://github.com/ThibaultGROUEIX/ChamferDistancePytorch)

 loss 对于三维特征的帮助性

如何去约束结果的几何一致性

follow RGBD-GAN
