# Rendering



## Non-differentiable Rendering

a discrete operation called rasterization





## Differentiable Rendering

a fundamental tool in computer graphics that convert 3D models into 2D images.



neural networks bring "neural rendering" because natural differentiable





---

Neural 3d mesh renderer

CVPR 2018

Differentiable Monte Carlo Ray Tracing through Edge Sampling

SIGGRAPH 2018

[Soft Rasterizer: A Differentiable Renderer for Image-based 3D Reasoning](https://arxiv.org/pdf/1904.01786.pdf)  
Shichen Liu, Tianye Li, Weikai Chen, Hao Li  
[ICCV 2019] ()



Opendr: An approximate differentiable renderer

ECCV 2014





Neural scene representation and rendering.

Science

[RenderNet: A deep convolutional network for differentiable rendering from 3D shapes](https://arxiv.org/pdf/1806.06575.pdf)  
Thu Nguyen-Phuoc, Chuan Li, Stephen Balaban, Yong-Liang Yang  
[NIPS 2018]



[Face-to-Parameter Translation for Game Character Auto-Creation](https://arxiv.org/pdf/1909.01064.pdf)  
*Tianyang Shi, Yi Yuan, Changjie Fan, Zhengxia Zou, Zhenwei Shi, Yong Liu*  
[ICCV 2019]







Dist: Rendering deep implicit signed distance function with differentiable sphere tracing

iterative ray marching to render a DeepSDF decoder

stratified random sampling 





## Volume Rendering

a set of $\mathcal{S}$ of sampled points per ray

A ray $x$ emanating from a camera position c in direction v 

x = c + tv 

volume rendering is approximating the integrated light radiance along this ray reaching the camera.




$$
\text{transparency: } T(t)=\exp \left(-\int_{0}^{t} \sigma(\boldsymbol{x}(s)) d s\right)
\\
\text{opacity: } O(t)=1-T(t)
\\
\text{PDF: } \tau(t)=\frac{d O}{d t}(t)=\sigma(\boldsymbol{x}(t)) T(t)
$$
the volume rendering is the expected light along the ray
$$
I(\boldsymbol{c}, \boldsymbol{v})=\int_{0}^{\infty} L(\boldsymbol{x}(t), \boldsymbol{n}(t), \boldsymbol{v}) \tau(t) d t
$$



can handle abrupt depth changes 

multiple points along the ray will effect the reconstruction, the gradient signals is full of the space rather than the thin surface.




## Surface Rendering

