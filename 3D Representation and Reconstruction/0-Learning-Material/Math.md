## eikonal equation

https://www.ljll.math.upmc.fr/hecht/ftp/Mireille-Haddad/distance.pdf



先给出所有定义：



$\Omega \subset \mathbb{R}^d$ 是一个有界区域 (bounded domain)，边界用 $\partial \Omega$ 表示，Signed distance function (SDF) 被定义为
$$
u_{\Omega}(x)= \begin{cases}-d(x, \partial \Omega) & \text { if } x \in \Omega \\ 0 & \text { if } x \in \partial \Omega \\ d(x, \partial \Omega) & \text { if } x \in \bar{c} \Omega\end{cases}
$$

> 这种记法是内部为负，外部为正。

以及距离 $d$ 的定义
$$
d(x, \partial \Omega)=\min _{y \in \partial \Omega}\|x-y\|
$$


如果假设边界是平滑的，且 $u(x)$ 可导，则有如下性质

- 对于边界上的点 $x \in \partial \Omega$，$\nabla u_{\Omega}(x)=n(x)$ ，其中 $n$ 是法向量
- 对于非边界上的点 $x \in \mathbb{R}^d \backslash \partial \Omega$，$\nabla u_{\Omega}(x)=\frac{p_x-x}{u_{\Omega}(x)}$ ，其中$p_x$ 是边界上距离 $x$ 最近的点
- 对于任意点都有，$\left\|\nabla u_{\Omega}(x)\right\|=1$，来自于Eikonal equation



证明：http://math.uchicago.edu/~may/REU2020/REUPapers/Miao,Jinghong.pdf

https://math.stackexchange.com/questions/3605929/signed-distance-function-and-the-eikonal-equation?rq=1





假设有一个内部空间，表示为 $\Omega$，整个点空间表示为 $X$，则Signed Distance Function (SDF) 可以定义为：
$$
f(x)=
\begin{cases}
d(x, \partial \Omega) & x \in \Omega \\ 
-d(x, \partial \Omega) & x \in \Omega^c
\end{cases}
$$
其中 $\partial \Omega$ 是边界，$d$ 是点 $x$ 距离边界的最短距离。



如果边界是平滑的，则会有 eikonal equation
$$
\sum_{i=1}^n\left(\frac{\partial u}{\partial x_i}\right)^2=1
$$


它的解是局部距离到一个超表面







从直觉上讲，f(x) = d
