# <p align=center>`Training & Testing Acceleration` </p>

A collection of resources on acceleration of neural radiance field.



## Contributing

Feedback and contributions are welcome! If you think I have missed out on something (or) have any suggestions (papers, implementations and other resources), feel free to pull a request or submit an issue. I will release the [latex-pdf version]() in the future. :arrow_down:markdown format:

``` markdown
[Paper Name](abs link)  
*[Author 1](homepage), Author 2, and Author 3*
**[`Conference/Journal Year`] (`Institution`)** [[Github](link)] [[Project](link)]
```

:smile: Now you can use this [script](https://github.com/yzy1996/Python-Code/tree/master/Python%2BarXiv) to automatically generate the above text.



## Introduction



训练和测试的加速是两个独立部分。



原始NeRF的训练速度在1-2天

This limits efﬁciency-critical applications.



首先要提的就是关于采样，首先看原先的采样是什么样的
$$
\boldsymbol{x}_i = r_o+ i\delta_cr_d
$$
就是均匀采i点，





$\alpha_i=1-\exp \left(-\sigma_i \delta_i\right)$ 

如果 这个值为0，就不算有效点，而在实验中无效点是有很多的



增加一个 momentum x，意思是


$$
V_\sigma [i] \leftarrow (1-\beta) \cdot V_\sigma[i] + \beta \cdot \sigma_c(\boldsymbol{x})
$$
所以在采样的时候，先判断一下 $V_\sigma[i] > 0$，然后

最终的提升效果是，有多少的有效比例，就能提高多少倍



到fine了，再增加一个阈值，





## Literature





### 1. Training 

PixelNeRF [36] 

introduces image features from ResNet [7] and skips training in novel scenes. But its synthesis accuracy reduces [2]. 

IBRNet [32] that integrates multi-view features in the weighted sum, thus improving accuracy.

MVSNeRF [2], which employs MVSNet [34] to provide a feature volume for NeRF. It can synthesize high-quality images within 15minute ﬁnetuning. 



However, the testing time of the above methods is as long as the original NeRF.



### 2. Testing

[(NSVF) Neural Sparse Voxel Fields](https://arxiv.org/abs/2007.11571)  
*Lingjie Liu, Jiatao Gu, Kyaw Zaw Lin, Tat-Seng Chua, Christian Theobalt*  
**[`arXiv 2020`]**  `[1 FPS]`

gives a hybrid scene representation that combines NeRF with sparse voxels structure. The generated sparse voxels guide and reduce sampling. It improves the inference speed to around . 



reduced the inference time by adopting around 1,000 tiny MLPs, where each MLP takes care of a speciﬁc 3D area. The running speed is over 10 FPS. 



[168 FPS] PlenOctree [35] and 

[200 FPS] FastNeRF [4] achieved inference speed over  and  respectively by caching the whole 3D scenes. We note that their training is still heavy. 

EfﬁcientNeRF achieves faster per-image inference speed along with far less training time.




[ACORN: Adaptive Coordinate Networks for Neural Scene Representation](https://arxiv.org/abs/2105.02788)  
*Julien N. P. Martel, David B. Lindell, Connor Z. Lin, Eric R. Chan, Marco Monteiro, Gordon Wetzstein*  
**[`SIGGRAPH 2021`]** 



[Neural Sparse Voxel Fields](https://arxiv.org/abs/2007.11571)  
*Lingjie Liu, Jiatao Gu, Kyaw Zaw Lin, Tat-Seng Chua, Christian Theobalt*  
**[`NeurIPS 2020`]** 

[Neural Geometric Level of Detail: Real-time Rendering with Implicit 3D Shapes](https://arxiv.org/abs/2101.10994)  
*Towaki Takikawa, Joey Litalien, Kangxue Yin, Karsten Kreis, Charles Loop, Derek Nowrouzezahrai, Alec Jacobson, Morgan McGuire, Sanja Fidler*  
**[`CVPR 2021`]** 

[FastNeRF: High-Fidelity Neural Rendering at 200FPS](https://arxiv.org/abs/2103.10380)  
*Stephan J. Garbin, Marek Kowalski, Matthew Johnson, Jamie Shotton, Julien Valentin*  
**[`ICCV 2021`]** 

[PlenOctrees for Real-time Rendering of Neural Radiance Fields](https://arxiv.org/abs/2103.14024)  
*Alex Yu, Ruilong Li, Matthew Tancik, Hao Li, Ren Ng, Angjoo Kanazawa*  
**[`ICCV 2021`]** 

[KiloNeRF: Speeding up Neural Radiance Fields with Thousands of Tiny MLPs](https://arxiv.org/abs/2103.13744)  
*Christian Reiser, Songyou Peng, Yiyi Liao, Andreas Geiger*  
**[`ICCV 2021`]** 

[Plenoxels: Radiance Fields without Neural Networks](https://arxiv.org/abs/2112.05131)  
*Alex Yu, Sara Fridovich-Keil, Matthew Tancik, Qinhong Chen, Benjamin Recht, Angjoo Kanazawa*  
**[`CVPR 2022`]** 


[Direct Voxel Grid Optimization: Super-fast Convergence for Radiance Fields Reconstruction](https://arxiv.org/abs/2111.11215)  
*Cheng Sun, Min Sun, Hwann-Tzong Chen*  
**[`CVPR 2022`]** 

[TensoRF: Tensorial Radiance Fields](https://arxiv.org/abs/2203.09517)  
*Anpei Chen, Zexiang Xu, Andreas Geiger, Jingyi Yu, Hao Su*  
**[`ECCV 2022`]** 

[Instant Neural Graphics Primitives with a Multiresolution Hash Encoding](https://arxiv.org/abs/2201.05989)  
*Thomas Müller, Alex Evans, Christoph Schied, Alexander Keller*  
**[`SIGGRAPH 2022`]** 







