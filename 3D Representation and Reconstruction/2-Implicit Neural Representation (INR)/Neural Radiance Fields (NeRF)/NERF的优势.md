可以保证 view-condidtency，

因为体密度只和坐标x有关





存在的问题呢？



**NeRF overfits to training views**

mimicking the image-formation process at observed poses -- from dietnerf



the optimal scene representation is underdetermined



Degenerate solutions





关于nerf的描述

NeRF[28] proposed optimizing scene radiance fields, representedusing global MLPs, from RGB images to achieve photorealisticnovel view synthesis. However, NeRF cannot handlelarge-scale scenes well due to its limited MLP networkcapacity and impractical slow per-scene optimization.





volumetric radiance field rendering consumes a lot of memory and often can only regress sparsely sampled pixels during training, and not the full image necessary for computing the VGG features used in many style losses.





Background of radiance fields







Deferred back-propagation 延迟反向传播



such rendering is very memory-inefficient in practice.

many methods randomly sample a sparse set of pixels for rendering

just for computing independently per-pixel, such as l1\l2 loss





for the deferred back-propagation, 



