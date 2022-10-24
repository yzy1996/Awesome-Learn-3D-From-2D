# Template

价值

fitting observation data, analyzing shape collections, and transferring shape attributes.

和deformation的关系



**mesh-based template**

A papier-mˆach´e approach to learning 3D surface generation.

**grids-based template**

FoldingNet: Point cloud auto-encoder via deep grid deformation





### DIT

[Deep Implicit Templates for 3D Shape Representation](https://arxiv.org/pdf/2011.14565.pdf)

**[`CVPR 2021 (Oral)`]**	**[`Tsinghua`]**

*Zerong Zheng, Tao Yu, Qionghai Dai, Yebin Liu*



![image-20210218154229986](https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20210218154240.png)

![image-20210218154436841](https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20210218154443.png)

> **Summary**

decomposes the implicit representations into a template implicit function and a continuous warping field

find a common structure 



> **Details**

The key idea is that the **shape variance** can be reflected by the differences of these SDFs relative to a template SDF that capture their **common structure**. 

Decompose the conditional signed distance function $\mathcal{F}$ into $\mathcal{F} = \mathcal{T} \circ \mathcal{W}$, i.e.,
$$
\mathcal{F}(\boldsymbol{p},\boldsymbol{c}) = \mathcal{T}\left(\mathcal{W}\left(\boldsymbol{p},\boldsymbol{c}\right)\right),
$$
where $\mathcal{W}: \mathbb{R}^3 \times \mathcal{X} \mapsto \mathbb{R}^3$ maps the coordinate of $\boldsymbol{p}$ to a new 3D coordinate, while $\mathcal{T}: \mathbb{R}^3 \mapsto \mathbb{R}$ outputs the signed distance value at this new 3D coordinate.



$\mathcal{W}$ is a conditional spatial warping function and transforms $\boldsymbol{p}$ to its **canonical position**

$\mathcal{T}$ is an implicit representing function and can be regarded as a common template SDF for a set of objects.

> the author say that in the strict sense of the term, a warping of an SDF is not an SDF in general. However, we adopt two constraints to make sure that the warped SDF can still approximate the target SDF: (1) we use truncated SDF that only varies in a small band near the surface, and (2) we normalize all the meshes into the same scale. Therefore, we loosely use the term "SDF" in this paper and regard a warping of an SDF as another SDF.



训练时困难的，可能带来的问题是学出来的模板可能很小，over-simplified implicit template

模板也需要具有形状的完整性和解释性，mesh interpolation and shape completion



> **Training**

K 个 shape, 每一个shape 有N个SDF samples



### DIF

[Deformed Implicit Field: Modeling 3D Shapes with Learned Dense Correspondence](https://arxiv.org/pdf/2011.13650.pdf)

**[`CVPR 2021`]**	**[`Tsinghua`]**

*Yu Deng, Jiaolong Yang, Xin Tong*



![image-20210221104214626](https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20210221104223.png)

 

> **Summary**

The goal is to generate 3D objects from one category

each different shape object represented by a latent space code $\alpha$ 

the generation is implemented by a neural model $f$

using SDF to represent shape for each coordinate $p$
$$
f: (\alpha, p) \in \mathbb{R}^{k+3} \mapsto s \in \mathbb{R}
$$
$\alpha, \mathbf{x}$ will intertwine, decompose into:
$$
\begin{array}{l}
\text{Hyper-Net} ~~~~ \Psi: \alpha \in \mathbb{R}^{k} \rightarrow \omega \in \mathbb{R}^{m} \\
\text{DIF-Net} ~~~~ \Phi_{\omega}: p \in \mathbb{R}^{3} \rightarrow s \in \mathbb{R}
\end{array}
$$
DIF-Net consist of two sub-networks: a template SDF generation network $T$ and a Deform-Net $D$.
$$
\begin{array}{l}
T: p \in \mathbb{R}^{3} \mapsto s^t \in \mathbb{R} \\
D_\omega: p \in \mathbb{R}^{3} \mapsto v \in \mathbb{R}^3
\end{array}
$$
<img src="https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/20210221151547.png" alt="image-20210221151546463" style="zoom:50%;" />

The insight is that the object instance are mostly composed by a few common patterns or semantic structures.
$$
d = T(p + v) = T(p + D_{\omega}(p))
$$
an extra correction field
$$
D_{\omega}: p \in \mathbb{R}^{3} \rightarrow(v, \Delta s) \in \mathbb{R}^{4}
$$
and rewrite
$$
s=T(p+v)+\Delta s=T\left(p+D_{\omega}^{v}(p)\right)+D_{\omega}^{\Delta s}(p)
$$
so the total model can be written as 
$$
f(\alpha, p)=\Phi_{\Psi(\alpha)}(p)=T\left(p+D_{\Psi(\alpha)}^{v}(p)\right)+D_{\Psi(\alpha)}^{\Delta s}(p)
$$



