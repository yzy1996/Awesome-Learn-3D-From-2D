# <p align=center>`Predict camera pose from images`</p>



## Introduction



random forests

RANSAC 

PoseNet



contrastive loss to produce pixel-wise descriptors



point-based SIFT



visual localisation systems SIFT or ORB use point landmark to localize.

these features are not able to deal with challenging real-world scenarios. not sufficiently robust



## Pose Representation

Euler angles, axis-angle, SO(3) rotation matrices and quaternions

- Euler angles

- axis-angle

- SO(3) rotation matrices

  over-parameterised

- quaternions

   https://krasjet.github.io/quaternion/quaternion.pdf

  https://www.youtube.com/watch?v=d4EgbgTm0Bg&t=1505s

  https://www.zhihu.com/question/23005815



## Loss function











## New idea



雾天去预测每增加环境干扰，对无人驾驶复杂环境有帮助









## Impact

autonomous vehicles







## Literature





### Related work

Multiple view geometry in computer vision





[(SfM) Modeling the World from Internet Photo Collections](http://phototour.cs.washington.edu/ModelingTheWorld_ijcv07.pdf)

[IJCV 2007]

> autonomously generate camera poses



[Scene Coordinate Regression Forests for Camera Relocalization in RGB-D Images](https://openaccess.thecvf.com/content_cvpr_2013/papers/Shotton_Scene_Coordinate_Regression_2013_CVPR_paper.pdf)  
**[`CVPR 2013`]**



[Geometric loss functions for camera pose regression with deep learning](https://arxiv.org/pdf/1704.00390.pdf)  
**[`CVPR 2017`] (`Cambridge`)**  
*Alex Kendall, Roberto Cipolla*



> introduce novel loss functions to reduce the gap in accuracy 
>
> re-projection error
>
> improve the performance of PoseNet



[PoseNet: A Convolutional Network for Real-Time 6-DOF Camera Relocalization](https://arxiv.org/pdf/1505.07427.pdf)  
**[`ICCV 2015`]**  
*Alex Kendall, Matthew Grimes, Roberto Cipolla*

> learns to regress the 6-DOF camera pose from a single image.
>
> but a naive loss function brings expensive tuning



[Deep Auxiliary Learning for Visual Localization and Odometry](https://arxiv.org/pdf/1803.03642.pdf)  
**[`ICRA 2018`]**  
*Abhinav Valada, Noha Radwan, Wolfram Burgard*

> Multi-Task Framework

