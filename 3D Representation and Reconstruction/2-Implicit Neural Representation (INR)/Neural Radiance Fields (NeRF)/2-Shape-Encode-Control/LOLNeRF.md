# 论文解读 LOLNeRF: Learn from One Look

[LOLNeRF: Learn from One Look](https://arxiv.org/abs/2111.09996)  
*Daniel Rebain, Mark Matthews, Kwang Moo Yi, Dmitry Lagun, Andrea Tagliasacchi*  
**[`CVPR 2022`] （`UBC, Google`)**



## 1. 简要概括

本文所针对的任务是**从单视角图像数据学3D形状**，即是从CelebA，FFHQ这样的数据集学到多视角生成。3D部分是借助的NeRF neural rendering，用AutoDecoder+latent code condition解决原版单场景的问题，用**预训练**的先验KeyPoint来提供训练中所需的相机参数（过去方法用structure-from-motion）。特点是**不用对抗训练（也就不需要训练全图），达到了相似的效果，节约了资源**。

主要贡献：1）实现了单视角的3DAD任务；2）为了实现这个任务采用预训练landmark对齐方式解决了相机参数问题；3）提高质量-优化了体密度采样&用segmenter。



| 论文写作优点                                                 |
| ------------------------------------------------------------ |
| Autodecoder里，比如训练1000张图，就需要先初始化1000个latent code，作者把这个定义成一个latent table，我写的话，可能就不会提及，觉得理所应当，而这样描述一下，并加上一个尺度大小，我看到的时候觉得是耳目一新。 |
| 在公式里用`\underbrace`加上这个 子Loss 是在第几章节会介绍的，清楚明了。 |
| Related work开头用序号交代了主要的topic，以及based的方法，清楚明了。 |



## 2. 主要流程图

![图片 1](https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/%E5%9B%BE%E7%89%87%201.jpg)

左图是粗略流程图，先通过图像得到相机参数，再condition on一个latent code z，一起送给NeRF，得到那一视角下的重建图，和原图进行loss对比，然后训练优化。最终学好的模型就能对新采样的z+d生成新视角图。右边是网络的主要设计，很直观不多介绍。



## 3. 方法解析

Loss就是这样简单的，第一个rgb就不多解释了，NeRF直接输出的颜色值
$$
\mathcal{L}_{\text {total }}=\mathcal{L}_{\text {rgb }}+\lambda_{\text {mask }} \mathcal{L}_{\text {mask }}+\lambda_{\text {hard }} \mathcal{L}_{\text {hard }}
$$

> 但文中提到说他的color不是相机角度的函数，有点费解？文中也没有更多的交代了。为了更简单吗，假设任意角度看过去颜色都是一样的！



### 3.1 前景分割

这算是一个加强的约束，不要有大的扭曲。纯色背景的就可以不用了。对于人脸采用 MediaPipe Selfie Segmentation 的预训练模型

$$
\mathcal{L}_{\text {mask }}=\mathbb{E}_{k \in\{1 \ldots K\}, \mathbf{p} \in I_k}\left[\left(\alpha\left(\mathbf{p} \mid \mathbf{z}_k\right)-S_I(\mathbf{p})\right)^2\right]
$$

> 对 $I_k$ 图采样像素 $\mathbf{p}$ 



### 3.2 优化体密度Sigma，加约束

拉普拉斯分布：一个非常尖峰的分布，类似于高斯，只不过高斯中间是平滑的，它这个更尖，概率上希望值落在中间最好，而中间的值就像高斯分布的均值一样，是预设的。如果追求稀疏的话，是可以用这个分布来约束，一个约束在0，一个约束在1，然后加和到一起，实现0，1约束。
$$
p(x) = e^{-|x|} + e^{-|1-x|}
\\
\mathcal{L}_\text{hard} = -\log(p)
$$



### 3.3 单视角图像是没有相机信息的

这是必须解决的问题，因为volume rendering 是需要相机参数的。它就通过给定一张图，用预训练模型标注5个特征点，因为都是人脸，所以只需要建立一个标准的3D模型，就能去比对这5个点，然后就知道相机角度了。

> 但这一点，nerf–这种可以一起估计相机参数了，因为分布区间很小，比较好估计。同时对比GAN模型，GAN就是可以增加相机的参数，用对抗去学。

具体的优化步骤：
$$
\underset{\mathbf{T}, \mathbf{K}}{\arg \min }\|\ell-P(\mathbf{p} \mid \mathbf{T}, \mathbf{K})\|^2
$$
采用 莱文伯格-马夸特方法 (Levenberg–Marquardt algorithm)：非线性最小化的数值解法。是高斯牛顿法的改进版。

对于汽车SRN数据集，他就用的数据集提供的信息。

**所以这一块是独立的，没有参与网络学习，不能太算贡献。**



### 3.4 怎么应对新采样呢？

truncation trick：通过调节 $\alpha$ 来控制多样性和质量。
$$
\text{truncated } z^\prime = \bar{z} + \alpha(z-\bar{z}), \quad \alpha<1
\\
\bar{w} \text{是均值}
$$
 provides a boost to the Inception Score and FID.



### 3.5 实验对比

- 比较生成的图像质量，用PSNR,SSIM,LPIPS

- 比较多视角的生成质量，用PSNR,SSIM,MAsk-LPIPS on HUMBI 数据集

- 比较深度估计，3DFAW数据集有真值，baseline是那些测深度的网络

Unsupervised learning of probably symmetric deformable 3D objects from images in the wild

(pi-GAN)Periodic Implicit Generative Adversarial Networks for 3D-Aware Image



## 4. 存在的疑问点

- 关于他的baseline选择pi-gan，而且还是在不同的数据集上比较的生成质量，存疑。

- 本文本来是对比对抗训练的方法，提出说不用对抗也能达到很好的效果，但结尾展望作者说未来可以结合对抗训练来提升质量:smile:，会不会有点矛盾。

- 本文并没有提及我们所认知的AD的优势，只说训练对像素点就行，不需要full image带来的训练成本问题

- 例如用实验验证训练集的数量和生成质量的关系，这是显然的呀，理论都可以证明，因为高度过拟合，虽然他把这一点放在附录了，但也是多此一举



## 5. 结束

3DAD(Autodecoder)是我之前一直在提的方案，首先这个框架十分的底层，很多人甚至都不屑于单独拎出来讲，所以核心在于怎么在它上面做文章。与本文类似的3D类别模型我们也已实现，但落地点不一样，导致文章的价值就有了差异。同时作者也提出了一些之前不知道的数值优化方法，增加了文章的深度吧（这一点在CVPR上可能也并不在意）。有很多文章感觉就做得很像，也是我完全能handle的，但就是没做出来人家这样solid的工作，需要学习人家的实验设计，怎么切分文章的落地task，然后再想着怎么结合已有的知识来解决它，这样就能算是一个好工作。