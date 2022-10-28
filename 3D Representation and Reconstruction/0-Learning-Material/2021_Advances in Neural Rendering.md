[Advances in Neural Rendering](https://arxiv.org/pdf/2111.05849.pdf)  
*Ayush Tewari, Justus Thies, Ben Mildenhall, Pratul Srinivasan, Edgar Tretschk, Yifan Wang, Christoph Lassner, Vincent Sitzmann, Ricardo Martin-Brualla, Stephen Lombardi, Tomas Simon, Christian Theobalt, Matthias Niessner, Jonathan T. Barron, Gordon Wetzstein, Michael Zollhoefer, Vladislav Golyanik*  
**[`arXiv 2021`]**



This SOTA report mainly focus on **neural rendering** methods that combine **classical rendering principles** with **neural scene representations**.  Towards the goal of synthesizing photo-realistic images from observations and in a controllable way.



Advantages:

- 3D-consistent by design



Review on the methods including:

- static & non-rigidly deforming scenes
- scene editing
- scene composition
- scene-specific & across category





标准的建模结构是需要表征各种场景信息（包括 相机，光照，材质）

nerf简化了步骤，仅仅表征3D场景，然后用一种积分渲染的方式来监督，



来自virtual camera
