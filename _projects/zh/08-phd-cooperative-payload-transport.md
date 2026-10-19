---
layout: page
title: "博士研究：多无人机协同绳系负载运输的控制理论与工程实现"
description: "基于多体动力学与李雅普诺夫方法的多无人机协同绳系负载运输非线性控制（JGCD、IEEE TIE、IEEE/ASME TMECH，引用超过300次），基于C++与ROS在Jetson Nano及Pixhawk上从零实现。"
lang: zh-CN
permalink: /zh/research/phd-cooperative-payload-transport/
category: 科研项目
featured: true # shown on the home page
importance: 8
cv_group: utias-phd
period: "2016/09至2021/03"
img: assets/img/projects/phd-payload-flight.jpg
card_img: assets/img/projects/phd-payload-card.jpg # home-page card only
---

**时间：** 2016/09至2021/03 · 博士，多伦多大学航空航天研究院 · 导师：Dr. Hugh H.T. Liu（刘洪涛教授）

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
    {% include youtube.liquid id='ejTnwAZaz20' title='Cooperative tethered-payload transportation with multiple quadrotors' %}
  </div>
</div>
<div class="caption">飞行实验：多架四旋翼无人机协同绳系负载运输。</div>

<!-- details -->

- 从事无人机自主运输系统的控制理论与工程实现研究。针对多无人机绳系负载的应用场景，提出了一整套基于多体动力学的非线性控制方法，实现了多无人机协同负载运输，并搭建实验平台验证了方案的工程可行性，为未来智慧城市中无人机协同运输的控制难题提供了解决方案。
- 该项目由加拿大自然科学与工程研究理事会（Natural Sciences and Engineering Research Council of Canada，NSERC）和Drone Delivery Canada公司共同资助，项目总金额为64万加元（约320万人民币）。
- 博士期间的杰出研究获得加拿大多伦多大学和安大略省政府全额奖学金：Ontario Trillium Scholarship（加拿大安大略省延龄草奖学金，全安大略省仅75人获得），奖学金共16万加元，约合人民币82万元。
- 在理论研究方面，提出了一套基于李雅普诺夫方法的非线性控制系统，并证明其在存在未知干扰的情况下能够保证绳系负载的稳定运输，为后续在恶劣天气下的负载安全运输提供了技术基础。学术成果发表于国际顶级期刊Journal of Guidance, Control, and Dynamics（航空类顶级期刊，JCR 1区）、IEEE Transactions on Industrial Electronics（机电自动化顶级期刊，中科院1区顶级期刊）和IEEE/ASME Transactions on Mechatronics（机电自动化顶级期刊，中科院1区顶级期刊）。目前相关工作已获得超过300次学术引用，得到了学术界的广泛认可（可参考[谷歌学术](https://scholar.google.ca/citations?hl=en&user=p2oGLVYAAAAJ)）。
- 在工程实现方面，从零开始自主实现了多无人机协同运输的非线性控制方法。使用C++和ROS编写飞行控制程序，在资源有限的机载电脑NVIDIA Jetson Nano上实现了实时飞行控制算法以及对Pixhawk飞控计算机的指令控制，为方法的工程落地提供了切实可用的软件方案，并在四旋翼无人机上验证了所提方法的正确性与容错控制能力。
- 项目视频和GitHub网站如下：
  - YouTube：<https://www.youtube.com/watch?v=ejTnwAZaz20>
  - GitHub：<https://github.com/LonghaoQian/px4_command>

<!-- end details -->

## 理论框架简介

<style>
  mjx-container[display="true"] {
    overflow-x: auto;
    overflow-y: hidden;
    padding: 0.25rem 0;
  }
</style>

负载、绳索与四旋翼被作为一个完整的多体系统进行建模与控制。带扰动估计器的分层非线性控制器使负载沿参考路径飞行，其稳定性由李雅普诺夫方法证明（JGCD，2022）。

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/phd-system-geometry.jpg" alt="多四旋翼吊挂负载系统的几何关系" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">系统几何关系：多架四旋翼通过长度为 l 的绳索吊运刚体负载，负载沿分段直线参考路径飞行。</div>

**1. 统一的多体模型。** 系统被分解为负载子系统 $$\Sigma_p$$（负载位姿、绳索方向及所有平动速度）和每架四旋翼的姿态子系统 $$\Sigma_j$$：

$$
\Sigma_p: \begin{cases} M\dot{u} + C u = G + F + \Delta \\ \dot{x}_p = v_p, \quad \dot{R}_{IP} = R_{IP}\,\omega_p^\times, \quad \dot{r}_j = v_j \end{cases}
\qquad
\Sigma_j: \begin{cases} J\dot{\omega}_j + \omega_j^\times J \omega_j = \tau_j \\ \dot{R}_{Ij} = R_{Ij}\,\omega_j^\times, \quad f_{L,j} = -f_j R_{Ij} e_3 \end{cases}
$$

其中 $$u = [\,v_p^\top\ \ \omega_p^\top\ \ v_1^\top \cdots v_N^\top\,]^\top$$ 由负载速度、角速度以及各绳端水平速度组成；$$M$$ 与 $$C$$ 为惯性矩阵与科氏矩阵；$$F$$、$$G$$、$$\Delta$$ 分别为升力、重力与扰动力。每根绳索向量为 $$L_j = [\,r_j^\top,\ -\sqrt{l^2 - r_j^\top r_j}\,]^\top$$，因此水平偏移 $$r_j$$ 即可完全描述绳索状态。

**2. 路径跟踪问题。** 负载应沿路径第 $$i$$ 段（起点 $$p_i$$、方向 $$n_i$$、期望速度 $$v_{d,i}$$）滑行，同时保持期望姿态 $$R_{IP,d}$$：

$$
e_{p,i} = (I - n_i n_i^\top)(x_p - p_i), \qquad e_{v,i} = v_p - v_{d,i}, \qquad e_r = \tfrac{1}{2}\big(R_{PI,d} R_{IP} - R_{PI} R_{IP,d}\big)^\vee .
$$

控制目标是使零误差状态渐近稳定。系统至少需要三架四旋翼：权重 $$a_j > 0$$ 满足 $$\sum_j a_j t_j = 0$$、$$\sum_j a_j = 1$$ 且 $$\operatorname{rank}\big(\sum_j a_j t_j^\times t_j^\times\big) = 3$$，从而在分配升力时不对负载产生额外力矩。

**3. 分层控制器。** 外环为虚拟控制律，计算每架四旋翼应产生的升力向量；内环为每架四旋翼上的姿态跟踪器，使其倾转以产生该升力。

<div class="row">
  <div class="col-sm-10 mx-auto mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/phd-control-diagram.png" alt="系统控制框图" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">控制框图：虚拟控制律给出每架四旋翼的升力向量，并由此提取推力与目标姿态，交由姿态控制器跟踪。</div>

引入滑模变量 $$s_p = e_{v,i} + k_v e_{p,i}$$ 与 $$s_r = \omega_p + k_r e_r$$，第 $$j$$ 架四旋翼的虚拟控制力为

$$
f_{v,j} = \hat{f}_{t,j} + \hat{f}_{0,j} + f_{a,j} + f_{b,j} + f_{c,j}, \qquad
f_{b,j} = -a_j\big(m_p \hat{\xi} + k_p m_p s_p\big), \qquad
f_{c,j} = -a_j R_{IP} E_j \big(J_p \hat{\eta} + k_\Omega s_r\big),
$$

其中 $$\hat{f}_{t,j}$$ 为平衡重力与估计扰动的配平力，$$\hat{f}_{0,j}$$ 使四旋翼与负载运动同步，$$f_{a,j}$$、$$f_{b,j}$$、$$f_{c,j}$$ 消除路径跟踪误差。每架四旋翼的推力为 $$f_j = \lVert f_{v,j} \rVert$$，并由几乎全局渐近稳定的姿态跟踪器跟踪由 $$f_{v,j}$$ 提取的目标姿态。

**4. 扰动估计（UDE）。** 风扰与模型误差由每架四旋翼实测加速度与模型力之间的差值经低通滤波估计得到：

$$
\hat{\Delta}_j = \int_0^t \kappa_j\, \mathfrak{B}_j \big( m_j \dot{v}_{q,j} - f_{L,j} - m_j g_I - \hat{\Delta}_j \big)\, d\tau, \qquad
\hat{\Delta}_{\perp,j} = \Big(I - \frac{L_j L_j^\top}{l^2}\Big)\hat{\Delta}_j .
$$

类似的更新律给出负载上的等效扰动力 $$\hat{\Delta}_T$$ 与力矩 $$\hat{\Delta}_R$$。其积分项累积路径跟踪误差，因此该估计器相当于一个具有稳定性保证的非线性PID控制器。

**5. 稳定性分析。** 李雅普诺夫函数由误差运动的动能、绳索倾角惩罚项、路径与姿态误差以及估计误差组成：

$$
V = V_1 + \sum_{j=1}^{N} a_j V_{2,j} + V_3 + V_4, \qquad
V_1 = \tfrac{1}{2}(u + u_d)^\top M (u + u_d), \qquad
V_3 = k_p k_v m_p\, e_{p,i}^2 + k_r k_\Omega \operatorname{tr}\big(I - R_{PI,d}^\top R_{PI}\big).
$$

其导数满足二次型上界

$$
\dot{V} \le -\sum_{j=1}^{N} a_j\, u_K^\top \begin{bmatrix} H_{K,j} & H_{K,\Delta} \\ H_{K,\Delta}^\top & H_{\Delta,j} \end{bmatrix} u_K \le 0 ,
$$

当增益使 $$H_{K,j}$$ 正定时成立。由LaSalle定理可得外环渐近稳定；由于姿态跟踪器几乎全局渐近稳定，利用约化定理可将结论推广到估计吸引域内的完整系统（论文定理1）。

## 飞行实验

实验在FSC OptiTrack实验室中使用三架S500四旋翼进行。14台OptiTrack相机测量四旋翼与负载的位姿，每架四旋翼上的NVIDIA Jetson Nano通过5 GHz Wi-Fi以50 Hz接收反馈。在下面的测试中，负载平台上额外放置了一个物体，使负载与其模型不再一致。

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/phd-added-mass-test.jpg" alt="负载平台附加物体的飞行测试" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">负载平台附加物体的飞行测试。(a) 测试场景。(b) x方向从 −0.3 m 到 0.6 m 阶跃指令下的负载位置（I），以及偏航从 −20° 到 20° 阶跃指令下的负载姿态（II）。两者均无稳态误差地收敛到指令值。</div>

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/phd-estimated-disturbances.png" alt="飞行测试中的扰动估计" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">同一测试中的扰动估计。(a) 负载上的等效扰动力与力矩：竖直方向的力随电池消耗而漂移，高频成分来自空气湍流与结构柔性。(b) 每架四旋翼上的扰动估计，主要由机体结构变形引起。</div>
