# <p align=center>`3D Object Manipulation` </p>

A collection of resources on 3D object manipulation with neural radiance field.



## Contributing

Feedback and contributions are welcome! If you think I have missed out on something (or) have any suggestions (papers, implementations and other resources), feel free to pull a request or submit an issue. I will release the [latex-pdf version]() in the future. :arrow_down:markdown format:

``` markdown
[Paper Name](abs link)  
*[Author 1](homepage), Author 2, and Author 3*
**[`Conference/Journal Year`] (`Institution`)** [[Github](link)] [[Project](link)]
```

:smile: Now you can use this [script](https://github.com/yzy1996/Python-Code/tree/master/Python%2BarXiv) to automatically generate the above text.



## Introduction

**[Background]** The recently rising advances of implicit volumetric representation blew us away in capturing 3D structures. Among these works, neural radiance fields (NeRF) utilize a volume rendering technique to render implicit neural representations (INR) for high-quality novel view synthesis, providing an ideal representation for 3D content.

**[Task]** Editing NeRF (e.g., deforming the shape or changing the appearance color) is an extraordinarily challenging but valuable task that energizes more exciting applications (e.g., 3D content re-creation). Hope to support users editing the attributes of 3D shape, and resulting photo-realistic rendering from novel views.

**[Obstacles]** Unlike 2D image manipulation, multi-view dependency of 3D objects makes it more difficult. The editing or control will be directly operated on the whole 3D representation, thus we can synthesize the novel view images of the edited scene without re-training the network.



## Methods & Literature

The core is to disentangle the latent shape and appearance code, different code determines different result.

To be solved:

- more freedom in shape manipulation
- fast inference
- friendly interactive manner



Conditional NeRF: train NeRF on a category of shapes and enables manipulation via latent space interpolations utilizing the pre-trained models.





### CLIP







里面也包含了 conditional nerf

- [GRAF: Generative Radiance Fields for 3D-Aware Image Synthesis](https://arxiv.org/pdf/2007.02442.pdf)  
  *Katja Schwarz, Yiyi Liao, Michael Niemeyer, Andreas Geiger*  
  **[`NeurIPS 2020`] (`MPI`)** [[Code](https://github.com/autonomousvision/graf)]  

- [pi-GAN: Periodic Implicit Generative Adversarial Networks for 3D-Aware Image Synthesis](https://arxiv.org/pdf/2012.00926.pdf)  
  *Eric R. Chan, Marco Monteiro, Petr Kellnhofer, Jiajun Wu, Gordon Wetzstein*  
  **[`CVPR 2021`] (`Stanford`)**  

- [pixelNeRF: Neural Radiance Fields from One or Few Images](https://arxiv.org/pdf/2012.02190.pdf)  
  *Alex Yu, Vickie Ye, Matthew Tancik, Angjoo Kanazawa*  
  **[`CVPR 2021`] (`UCB`)**  

- [GRF: Learning a General Radiance Field for 3D Scene Representation and Rendering](https://arxiv.org/pdf/2010.04595.pdf)  
  *Alex Trevithick, Bo Yang*  
  **[`ICCV 2021`] (`Williams, Oxford, PolyU`)**  

- [CodeNeRF: Disentangled Neural Radiance Fields for Object Categories](https://arxiv.org/pdf/2109.01750.pdf)  
  *Wonbong Jang, Lourdes Agapito*  
  **[`ICCV 2021`] (`UCL`)** 

- [Editing Conditional Radiance Fields](https://arxiv.org/pdf/2105.06466.pdf)  
  *Steven Liu, Xiuming Zhang, Zhoutong Zhang, Richard Zhang, Jun-Yan Zhu, Bryan Russell*  
  **[`ICCV 2021`] (`MIT, Adobe`)**

- [NeRFactor: Neural Factorization of Shape and Reflectance Under an Unknown Illumination](https://arxiv.org/pdf/2106.01970.pdf)  
  Xiuming Zhang, Pratul P. Srinivasan, Boyang Deng, Paul Debevec, William T. Freeman, Jonathan T. Barron  
  **[`Arxiv 2021`] (`MIT`)**
  
- [NeRF-Editing: Geometry Editing of Neural Radiance Fields](https://arxiv.org/abs/2205.04978)  
  *Yu-Jie Yuan, Yang-Tian Sun, Yu-Kun Lai, Yuewen Ma, Rongfei Jia, Lin Gao*  
  **[`CVPR 2022`] (`CAS`)**
  
- [SPAGHETTI: Editing Implicit Shapes Through Part Aware Generation](https://arxiv.org/abs/2201.13168)  
  *Amir Hertz, Or Perel, Raja Giryes, Olga Sorkine-Hornung, Daniel Cohen-Or*  
  **[`arXiv 2022`] (`Tel Aviv University`)**

- [AE-NeRF: Auto-Encoding Neural Radiance Fields for 3D-Aware Object Manipulation](https://arxiv.org/abs/2204.13426)  
  *Mira Kim, Jaehoon Ko, Kyusun Cho, Junmyeong Choi, Daewon Choi, Seungryong Kim*  
  **[`arXiv 2022`] (`Korea University`)**



[CLIP-NeRF: Text-and-Image Driven Manipulation of Neural Radiance Fields](https://arxiv.org/abs/2112.05139)  
*Can Wang, Menglei Chai, Mingming He, Dongdong Chen, Jing Liao*  
**[`CVPR 2022`] (`CityU`)**

[LOLNeRF: Learn from One Look](https://arxiv.org/abs/2111.09996)  
*Daniel Rebain, Mark Matthews, Kwang Moo Yi, Dmitry Lagun, Andrea Tagliasacchi*  
**[`CVPR 2022`]**
