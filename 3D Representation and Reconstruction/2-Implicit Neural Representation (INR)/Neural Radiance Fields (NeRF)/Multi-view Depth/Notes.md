# <p align=center>`Depth Prediction`</p>



[NerfingMVS: Guided Optimization of Neural Radiance Fields for Indoor Multi-view Stereo](https://arxiv.org/pdf/2109.01129.pdf)  
**[`ICCV`] (`Tsinghua`)**  
*Yi Wei, Shaohui Liu, Yongming Rao, Wang Zhao, Jiwen Lu, Jie Zhou*

<details><summary>Click to expand</summary>
<div align=center><img width="700" src="https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20210907203510.png"/></div>

> Summary

Mainly for predict the depth of the scene images.

> **Details**

Depth prior:

还有额外的自适应

employ the scale-invariant loss
$$
L\left(D_{p}^{i}, D_{S f M}^{i}\right)=\frac{1}{n} \sum_{j=1}^{n} | \log D_{p}^{i}(j)-\log D_{S f M}^{i}(j) +\alpha\left(D_{p}^{i}, D_{S f M}^{i}\right) |
$$




Guided optimization



因为NeRF采样是均匀的，因此很多细节深度，模棱两可的点是无法被区分的，因此本篇论文加入了一个深度的先验信息，来指导NeRF的采样。这样能给NeRF带来准确的深度信息。

</details>

---

