Injecting 3D Perception of Controllable NeRF-GAN into StyleGAN for Editable Portrait Image Synthesis





为什么我们要研究3DGAN是因为过去的2DGAN已经效果很好了，但因为确实3D的理解，因此会缺乏3D 一致性

因此为了解决这个问题，诞生了很多3D GAN 的尝试，

他们中间的一条路径是编辑，

The controllability and interpretability of 3D GANs have not been well explored.



In this work, 



3D信息可以通过类似于 3DMM 的形式

但就需要监督信号



project 3D objects on a 2D plane

一个共识是过去的2D GAN缺失了3D信息

就像归纳偏置一样，如果很难直接学的话，我们可以加入一些新的约束



2D GAN 的特点就是他是直接从图像中学的

2D GAN that is trained on RGB images only



## Related Work

> pose disentangled GANs



implicit 3D feature projection- but they allow only implicit 3D control and show blurry results.

- HoloGAN: Unsupervised
- BlockGAN

differentiable renderer- but they struggle with photorealism, high-resolution [47] and real image editing

- Do 2d gans know 3d shape?
- Lifting 2d stylegan for 3d-aware face generation





