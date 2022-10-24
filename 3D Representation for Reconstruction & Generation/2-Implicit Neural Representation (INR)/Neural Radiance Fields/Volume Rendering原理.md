**相关文献**

Kajiya, J.T., Herzen, B.P.V.: Ray tracing volume densities. Computer Graphics (SIGGRAPH) (1984)

Max, N.: Optical models for direct volume rendering. IEEE Transactions on Visualization and Computer Graphics (1995)

https://www.youtube.com/watch?v=otly9jcZ0Jg&ab_channel=NeuralRendering

![image-20220715163557865](https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/image-20220715163557865.png)



首先原文中出现的公式有这样两个：
$$
\begin{gather}
\text{连续化：} \quad C(\mathbf{r})=\int_{t_{n}}^{t_{f}} T(t) \sigma(\mathbf{r}(t)) \mathbf{c}(\mathbf{r}(t), \mathbf{d}) d t, \text { where } T(t)=\exp \left(-\int_{t_{n}}^{t} \sigma(\mathbf{r}(s)) d s\right)
\\
\text{离散化：} \quad \hat{C}(\mathbf{r})=\sum_{i=1}^{N} T_{i}\left(1-\exp \left(-\sigma_{i} \delta_{i}\right)\right) \mathbf{c}_{i}, \text { where } T_{i}=\exp \left(-\sum_{j=1}^{i-1} \sigma_{j} \delta_{j}\right)
\\
\text{其中 } \delta_{i}=t_{i+1}-t_{i} \text{ 是两个相邻采样点间的距离}
\end{gather}
$$




NeRF 原文中将 volume density $\sigma(\boldsymbol{x})$ 解释为：

> The volume density $\sigma(\boldsymbol{x})$ can be interpreted as the differential probability of a ray terminating at an infinitesimal particle at location x. 体积密度$\sigma(\boldsymbol{x})$ 可以解释为在位置x处无穷小粒子终止的射线的微分概率密度。




The function T(t) denotes the accumulated transmittance along the ray fromtn to t, i.e., the probability that the ray travels from tn to t without hittingany other particle.



![image-20220713160847927](https://raw.githubusercontent.com/yzy1996/Image-Hosting/master/image-20220713160847927.png)



一个3D shape在空间中，我们将它假想成是由一系列粒子构成的，就像点云一样吧

相机的光线是射向这些粒子的

每穿过一个粒子，这个光线的能量就要衰减一次






> 有效区间需要给出概念，P(hit at t) = $\sigma(t)dt$ 
>
> 光线，颜色，粒子的关系



首先我们要表示的场景，可以看成是一团由无限小的彩色粒子组成的云 (a cloud of tiny colored particles)。

相机发出光束 $\mathbf{r}(t)=\mathbf{O}+t \mathbf{d}$ 射向这团粒子云，当光束碰到位于 $t$ 位置的粒子时，会返回这个粒子的颜色 $\mathbf{c}(t)$。光束的有效距离区间是 $[t_{\text{near}}, t_{\text{far}}]$，粒子在这个区间上服从 $p \sim \sigma(t)$，$\sigma(t)$ 即粒子密度；在 $t$ 位置粒子是否存在是不确定的，因此可以用一个概率来衡量，我们不能说落在 $t$ 那一点的概率，只能说落在 $t$ 微小邻域的概率，即表示为 $P(t邻域存在粒子) = \sigma(t)dt$。这个概率等同于光束能碰到这个粒子 $P(\text{光束碰到t邻域}) = \sigma(t)dt$。

粒子 $t$ 要把它的颜色 $\mathbf{c}(t)$ 沿着光束返回相机仅靠粒子本身是不足以成功的，还要看它的前面（靠近相机端）有没有障碍，有没有被其他粒子遮挡。所以我们需要用一个量来刻画遮挡量，也可以说是光线的衰减量，因为光束每穿过一个粒子，它的能量就会衰减；或者说光线上越往后的粒子越不容易表现出它的颜色。（透射率，透光率，内部透射率是指吸收造成的能量损失， 是一个累积量，越远越不容易透过 ，衡量光束能量最后还剩多少，出发点是1，最后是0）

那么什么最重要，是**光束第一次碰到的粒子点**，即光束上最靠近相机的粒子点是最重要的。我们是对 全局建模，因此直接去描述 粒子 $t$ 是被光束第一次碰到的概率 $P(\text{光束第一次碰到t邻域}) = P(t\text{之前光束没有碰到其他粒子}) \times P(\text{光束碰到t邻域})$。

后者是我们已经建模了的，只需要建模前者，我们用 $T(t)$ 来表示，即 $T(t) = P(t\text{之前光束没有碰到其他粒子})$。

为了表示 $T(t)$ ，我们可以用一个技巧：
$$
\begin{align}
P(\text{t+dt之前光束没有碰到其他粒子}) &= P(t\text{之前光束没有碰到其他粒子}) \times P(光束没有碰到t邻域)
\\
T(t+dt) &= T(t) \times (1 - \sigma(t)dt) \\
\text{微分展开} \quad T(t) + T^\prime(t)dt &= T(t) - T(t)\sigma(t)dt \\
\text{重新排布} \quad \frac{T^\prime(t)}{T(t)} &= - \sigma(t) \\
\text{积分} \quad \log T(t) &= \int_{t_0}^t - \sigma(t)dt \\
\text{指数} \quad T(t) &= \exp(\int_{t_0}^t - \sigma(t)dt) 
\end{align}
$$
我们回到前面想表达的 $P(\text{光束第一次碰到t邻域}) = T(t)\sigma(t)dt$

再加上粒子 $t$ 的颜色，就是 $P(粒子t贡献了颜色) = T(t)\sigma(t)\mathbf{c}(t)dt$。这样所有粒子贡献的颜色就是一个积分，
$$
\int_{t_\text{near}}^{t_\text{far}} T(t) \sigma(t) \mathbf{c}(t) d t
$$

> 这里的理解可能有点绕，既可以说后面粒子的贡献的概率，也可以说把每个粒子都看成是首次碰到的概率









> 为什么会有dt，是看成在t周围有一个小区间。这样才从概率密度到了概率，因为概率是概率密度的积分，一小点上的概率
>
> 对这个P积分的含义是，$\int_{0}^a \sigma (t)dt$   $P(X = x+ dx) = \sigma(x) dx $
>
> 有点落在这条光束上的概率，因为累积分布函数的表达是 $F(x) = P(X \le x)$
>


$$
\begin{align}
\int T(t) \sigma(t) \mathrm{c}(t) d t &\approx \sum_{i=1}^{n} \int_{t_{i}}^{t_{i+1}} T(t) \sigma_{i} \mathrm{c}_{i} d t \\
\text{Substitute} &= \sum_{i=1}^{n} T_{i} \sigma_{i} \mathbf{c}_{i} \int_{t_{i}}^{t_{i+1}} \exp \left(-\sigma_{i}\left(t-t_{i}\right)\right) d t \\
&=\sum_{i=1}^{n} T_{i} \sigma_{i} \mathbf{c}_{i} \frac{\exp \left(-\sigma_{i}\left(t_{i+1}-t_{i}\right)\right)-1}{-\sigma_{i}} \\
&=\sum_{i=1}^{n} T_{i} \mathbf{c}_{i}\left(1-\exp \left(-\sigma_{i} \delta_{i}\right)\right)
\end{align}
$$

$$
\text { For } t \in\left[t_{i}, t_{i+1}\right], T(t)=\exp \left(-\int_{t_{1}}^{t_{i}} \sigma_{i} d s\right) \exp \left(-\int_{t_{i}}^{t} \sigma_{i} d s\right)
$$

$$
\exp \left(-\sum_{j=1}^{i-1} \sigma_{j} \delta_{j}\right)=T_{i} \quad \exp \left(-\sigma_{i}\left(t-t_{i}\right)\right)
$$

衡量被前面部分遮挡的有多少 | 又有多少被现在这块遮挡了





可以单独拎出来看 $\alpha_i = 1 - \exp(-\sigma_i \delta_i)$，traditional alpha compositing  

这样我们前面的表达式，substitute that back into the equations we jus tderived 可以写成
$$
\text{color} =\sum_{i=1}^{n} T_{i} \alpha_{i} \mathbf{c}_{i}=\sum_{i=1}^{n} T_{i} \mathbf{c}_{i}\left(1-\exp \left(-\sigma_{i} \delta_{i}\right)\right)
\\
T_{i}=\prod_{j=1}^{i-1}\left(1-\alpha_{j}\right)=\exp \left(-\sum_{j=1}^{i-1} \sigma_{j} \delta_{j}\right)
$$
这样是可以和很多其他渲染技术统一的



