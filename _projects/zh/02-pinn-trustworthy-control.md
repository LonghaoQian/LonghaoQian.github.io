---
layout: page
title: "基于物理信息神经网络（PINN）的可信AI控制框架"
description: "无需训练数据集、严格满足稳定性理论要求的PINN控制网络；结合黎曼流形与收缩分析的鲁棒控制收缩度量（RCCM）。成果已被CDC 2026与AIAA 2027 SciTech Forum录用。"
lang: zh-CN
permalink: /zh/research/pinn-trustworthy-control/
category: 科研项目
featured: true # shown on the home page
importance: 2
cv_group: utias-postdoc
period: "2025/08至2026/03"
img: assets/img/projects/ccm-payload-gate-thumb.jpg
card_img: assets/img/projects/ccm-training-framework.png # home-page card only
card_video: assets/video/ccm-payload-gate-sim-card.mp4 # home-page card only
card_video_poster: assets/img/projects/ccm-payload-gate-sim-card-poster.jpg
---

**时间：** 2025/08至2026/03 · 多伦多大学航空航天研究院

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/ccm-training-framework.png" alt="神经对偶CCM与神经反馈控制器的训练框架" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
    <figure>
      <video
        src="{{ 'assets/video/ccm-payload-gate-sim.mp4' | relative_url }}"
        poster="{{ 'assets/img/projects/ccm-payload-gate-sim-poster.jpg' | relative_url }}"
        class="img-fluid rounded z-depth-1"
        autoplay
        loop
        muted
        playsinline
      ></video>
    </figure>
  </div>
</div>
<div class="caption">左：根据系统动力学联合训练神经对偶CCM与神经反馈控制器。右：在学习得到的收缩控制器作用下，三架无人机通过变长度绳索吊运刚体负载穿越门框的仿真。</div>

<!-- details -->

- 领导两人团队（1博士、1硕士），提出一种基于物理信息神经网络（Physics-Informed Neural Networks，PINNs）的非线性控制训练方法，使神经网络能够在完全没有训练数据集的情况下，根据系统的多体动力学方程自动生成鲁棒控制算法，实现复杂系统控制方案的快速生成。相比于传统的机器学习控制，PINN生成的控制方法严格满足控制稳定性的理论要求，实现了基于神经网络的可靠控制方案。
- 通过微分几何，将PINN与黎曼流形理论相结合，实现了对无人机及机器人空间姿态的无奇异控制。结合收缩分析（Contraction Analysis）控制理论，将鲁棒控制问题转化为偏微分方程求解问题，进而使用PINN求解偏微分方程，实现具备稳定性保证的控制网络。
- 首次提出将PINN与黎曼流形相结合的鲁棒控制理论（鲁棒控制收缩度量，Robust Control Contraction Metrics，RCCM），在系统存在外界未知扰动和参数不确定的情况下，仍能保证控制精度。
- 本研究提出的基于PINN的AI控制框架可广泛应用于无人系统控制和具身智能控制中。
- 成果已被国际控制领域顶级会议IEEE Conference on Decision and Control（CDC 2026）和AIAA 2027 SciTech Forum录用，参考学术成果：“Neural Robust Control on Lie Groups Using Contraction Methods”（CDC 2026）、“Contraction-based Neural Control for Cooperative Aerial Payload Transportation with Variable-length Cables”（AIAA 2027 SciTech Forum）。

<!-- end details -->

## 理论框架简介

<style>
  mjx-container[display="true"] {
    overflow-x: auto;
    overflow-y: hidden;
    padding: 0.25rem 0;
  }
</style>

两篇论文的核心思路一致：将稳定性要求转化为关于黎曼度量的条件，再由神经网络在采样状态上同时求解满足这些条件的度量与控制器。整个过程不需要示教数据，只需要系统的运动方程。

### 背景知识

**A. 什么是收缩分析。** 李雅普诺夫分析关心轨迹是否收敛到某一个平衡点；收缩分析（Lohmiller与Slotine，1998）提出了更强的问题：*任意两条*相邻轨迹是否彼此收敛？它研究微分（虚拟）动力学 $$\delta\dot{x} = A(x)\,\delta x$$（其中 $$A = \partial f / \partial x$$），并用黎曼度量 $$M(x) \succ 0$$ 衡量 $$\delta x$$ 的长度。若该长度以统一速率 $$\lambda$$ 衰减，

$$
\frac{d}{dt}\big(\delta x^\top M(x)\,\delta x\big) \le -2\lambda\, \delta x^\top M(x)\,\delta x
\quad \Longleftrightarrow \quad
\dot{M} + \langle M A \rangle + 2\lambda M \preceq 0 ,
$$

则所有轨迹以指数速度彼此收敛。当 $$\underline{m} I \preceq M \preceq \overline{m} I$$ 时，

$$
\lVert x_1(t) - x_2(t) \rVert \le \sqrt{\overline{m}/\underline{m}}\; e^{-\lambda t}\, \lVert x_1(0) - x_2(0) \rVert .
$$

**为什么用于控制。**

- _跟踪而不只是镇定。_ 既然所有轨迹彼此收敛，系统就会收敛到规划器给出的任意可行参考轨迹 $$(x^*, u^*)$$，无需为每条轨迹重新构造李雅普诺夫函数。
- _逐点条件。_ 稳定性证书是每个状态 $$x$$ 上的矩阵不等式，可以在采样状态上逐一检验，或作为损失函数逐点惩罚，这正是神经网络训练所需要的形式。
- _可量化的鲁棒性。_ 扰动作为额外输入进入微分动力学，从而得到明确的增益上界和误差管道，而不只是定性的“稳定”结论。

**B. 控制收缩度量（CCM）。** Manchester与Slotine（2017）将收缩理论推广到带输入的系统 $$\dot{x} = f(x) + B(x)u$$。CCM是这样一种度量：存在微分反馈 $$\delta u = K(x)\,\delta x$$ 使闭环系统收缩，即 $$\dot{M} + \langle M(A + BK) \rangle + 2\lambda M \preceq 0$$。引入对偶度量 $$W = M^{-1}$$，并令 $$B_\perp$$ 张成控制输入无法作用的方向（$$B_\perp^\top B = 0$$），可得到与 $$u$$ 无关的充分条件：

$$
B_\perp^\top \Big( -\partial_f W + \big\langle \tfrac{\partial f}{\partial x} W \big\rangle + 2\lambda W \Big) B_\perp \prec 0,
\qquad
\partial_{b_i} W - \big\langle \tfrac{\partial b_i}{\partial x} W \big\rangle = 0 .
$$

第一个条件要求系统在控制器无法作用的方向上自行收缩；第二个条件要求度量沿控制输入方向保持不变（$$b_i$$ 为Killing向量场），从而控制器能够使这些方向收缩。只要这样的度量存在，就存在能跟踪任意可行轨迹的控制器。鲁棒版本（RCCM；Manchester与Slotine，2018）进一步引入扰动输入，把收缩性转化为下文使用的 $$\mathcal{L}_\infty$$ 增益上界。

**C. 李群。** 李群是同时具有群结构的光滑流形。无人机、负载或机器人连杆的姿态都是旋转：

$$
SO(3) = \{\, R \in \mathbb{R}^{3\times 3} : R^\top R = I_3,\ \det R = 1 \,\},
\qquad
\dot{R} = R\, \omega^\wedge ,
$$

其中 $$\omega^\wedge$$ 是角速度 $$\omega$$ 的反对称矩阵。欧拉角等坐标表示存在缺陷：俯仰角为 $$\pm 90^\circ$$ 时出现奇异（万向节锁），且会扭曲距离；四元数则对每个旋转有两种表示。直接在群上建模则全局有效。任何李群都是*可平行化*的：在任意 $$R$$ 处的速度都可写成 $$R\,\xi^\wedge$$（$$\xi \in \mathbb{R}^3$$），因此存在一个处处张成切空间的光滑基 $$S(x)$$，任意切向量都可写成 $$\delta x = S(x)\,v$$，其中 $$v$$ 为内蕴坐标。

**D. 为什么CCM需要李群视角。** CCM理论建立在 $$\mathbb{R}^n$$ 上。用 $$R$$ 的9个元素存储的旋转只有3个自由度，若在 $$\mathbb{R}^9$$ 上使用欧氏度量，就必须在另外6个离开 $$SO(3)$$、没有物理意义的方向上也满足收缩条件。两篇论文改为在内蕴坐标 $$v$$ 下描述微分动力学，只在切空间上寻找更低维的度量 $$\mathcal{M}(x)$$，再通过投影 $$P_S = S(S^\top S)^{-1}$$ 提升回原空间：

$$
\delta x = S\,v, \qquad B = S\,E, \qquad B_w = S\,E_w, \qquad M(x) = P_S(x)\, \mathcal{M}(x)\, P_S(x)^\top .
$$

由此，稳定性证书对任意姿态都成立且无奇异。误差以流形上的距离衡量，旋转误差采用李代数误差 $$\varepsilon_r = \tfrac{1}{2}\big(R^{*\top} R - R^\top R^*\big)^\vee$$。矩阵条件的维数也随之降低：三机协同负载系统的状态是嵌入在 $$\mathbb{R}^{30}$$ 中的24维流形，因此神经网络学习的是 $$24\times 24$$ 而非 $$30\times 30$$ 的度量。

### 主要成果

**1. 李群上的系统。** 系统状态位于流形 $$\mathcal{X}$$ 上（例如四旋翼的 $$\mathbb{R}^3 \times SO(3)$$ 及其速度），扰动为 $$w$$，输出为 $$z$$，控制律围绕参考轨迹 $$(x^*, u^*)$$ 设计：

$$
\dot{x} = f(x) + B(x)\,u + B_w(x)\,w, \qquad z = g(x,u), \qquad u = k(x,x^*) + u^* .
$$

与D中相同，微分长度在切空间上度量：$$V = v^\top \mathcal{M}(x)\, v$$，其中 $$\delta x = S(x)\,v$$。

**2. 鲁棒控制收缩度量（RCCM）。** 若存在一致有界的度量 $$\mathcal{M}(x)$$ 及常数 $$\lambda, \mu > 0$$，使得

$$
R_1 = \begin{bmatrix} \dot{\mathcal{M}} + \langle \mathcal{M}\mathcal{A} \rangle + 2\lambda\mathcal{M} & \mathcal{M}E_w \\ E_w^\top \mathcal{M} & -\mu I_p \end{bmatrix} \preceq 0,
\qquad
R_2 = \begin{bmatrix} 2\lambda\mathcal{M} - \alpha^{-1}\mathcal{C}^\top\mathcal{C} & 0 \\ 0 & (\alpha-\mu) I_p \end{bmatrix} \succeq 0,
$$

则闭环系统从扰动到输出具有 $$\mathcal{L}_\infty$$ 增益 $$\alpha$$。其中 $$\mathcal{A}$$ 与 $$\mathcal{C}$$ 为内蕴坐标下的闭环微分动力学与输出映射。

**3. 理论保证。** 跟踪误差由扰动大小界定：

$$
\lVert z - z^* \rVert^2_{\mathcal{L}_\infty^{[0,T]}} \le \alpha^2 \, \lVert w - w^* \rVert^2_{\mathcal{L}_\infty^{[0,T]}} + \beta\big(x(0), x^*(0)\big),
$$

因此在暂态过后，输出始终位于参考轨迹附近的管道 $$\Omega(z^*) = \{\, y : \lVert y - z^* \rVert \le \alpha \bar{w} \,\}$$ 之内。

**4. 用神经网络学习稳定性证书。** 控制器与对偶度量 $$\mathcal{W} = \mathcal{M}^{-1}$$ 均由神经网络表示，其结构保证 $$k_{nn}(x,x) = 0$$ 与 $$\mathcal{W} \succeq \overline{m}^{-1} I$$ 自动成立：

$$
k_{nn}(x,x^*) = K_1(x,x^*;\theta_{k_1}) \tanh\!\big(K_2(x,x^*;\theta_{k_2})\, \varepsilon(x,x^*)\big), \qquad
\mathcal{W}(x) = \Theta(x;\theta_w)^\top \Theta(x;\theta_w) + \overline{m}^{-1} I .
$$

二者在工作区域内的采样状态上联合训练，损失函数惩罚对上述条件的任何违反：

$$
\mathcal{L}_k = \mathrm{L_{PD}}(-R_1) + \mathrm{L_{PD}}(R_2) + \mathrm{L_{PD}}(-C_1) + \sum_i \lVert C_{2,i} \rVert_F + \sum_j \lVert C_{3,j} \rVert_F
+ \mathrm{L_{PD}}(\underline{m}^{-1} I - \mathcal{W}) + \mathrm{ReLU}(\alpha - \underline{\alpha}),
$$

其中 $$\mathrm{L_{PD}}$$ 惩罚非半正定矩阵，$$C_1$$ 要求无控系统在控制输入无法作用的方向上收缩，$$C_{2,i}, C_{3,j}$$ 要求控制输入与扰动方向为度量的Killing向量场（CDC 2026）。

<div class="row">
  <div class="col-sm-8 mx-auto mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/ccm-trajectory-comparison.png" alt="轨迹跟踪对比" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">从同一初始位置出发的四旋翼轨迹跟踪仿真：参考轨迹、几何控制器、CCM、RCCM以及带UDE的RCCM。</div>

**5. 应用：变长度绳索多无人机协同负载运输（AIAA SciTech 2027）。** 对于三架无人机吊运刚体负载的系统，运动方程被整理为负载与绳长分别由独立控制通道驱动的解耦形式。负载子系统 $$\Sigma_p$$（状态空间为 $$\mathbb{R}^{21} \times SO(3)$$）采用神经CCM控制器，满足

$$
C_{CCM} = \dot{\mathcal{M}} + \langle \mathcal{M}\mathcal{A} \rangle + 2\lambda\mathcal{M} \preceq 0,
$$

而绳长子系统是一个简单的双积分器，由独立的绳长跟踪器控制：

$$
\Sigma_l: \quad \frac{d}{dt}\begin{bmatrix} l \\ \dot{l} \end{bmatrix} = \begin{bmatrix} \dot{l} \\ 0 \end{bmatrix} + \begin{bmatrix} 0 \\ I_N \end{bmatrix} \tilde{f}_{\parallel},
$$

因此编队可以通过收短绳索穿越高度受限的门框，如上方仿真所示。

<div class="row">
  <div class="col-sm-8 mx-auto mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/ccm-payload-geometry.png" alt="变长度绳索多无人机负载系统几何关系" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">系统几何关系：四旋翼、滑轮驱动的变长度绳索以及刚体负载。</div>
