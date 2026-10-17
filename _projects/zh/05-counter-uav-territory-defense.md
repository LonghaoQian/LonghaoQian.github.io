---
layout: page
title: "基于强化学习的无人机区域安全和反无人机拦截算法研究"
description: "仅依赖无线电到达角测量的无人机集群自主防守与拦截：基于MADDPG的主动定位策略与基于RNN的HA-RMAPPO训练框架。成果发表于Science China Technological Sciences。"
lang: zh-CN
permalink: /zh/research/counter-uav-territory-defense/
category: 科研项目
featured: true # shown on the home page
importance: 5
cv_group: utias-postdoc
period: "2024/09至今"
img: assets/img/projects/cuas-thumb.jpg
card_img: assets/img/projects/cuas-card.jpg # home-page card only
---

**时间：** 2024/09至今 · 多伦多大学航空航天研究院

<div class="row mt-3">
  <div class="col-sm-8 mt-3 mt-md-0 d-flex align-items-center">
    {% include figure.liquid path="assets/img/projects/cuas-ctde-framework.png" alt="HA-RMAPPO集中训练、分散执行框架" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/cuas-rollout-7v3-aoa20.png" alt="到达角噪声下七架防守无人机对三架入侵无人机" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
  左：集中训练、分散执行（CTDE）的HA-RMAPPO框架。每架防守无人机拥有独立的Actor网络（MLP编码器、GRU、MLP输出头），集中式Critic指导训练，训练数据来自并行环境。右：在测试的最大到达角噪声
  σ₀ = 20° 下，七架防守无人机（绿）对三架入侵无人机（蓝）的第二阶段仿真。灰色椭圆为3σ位置置信区域；该次仿真以入侵者突破告终。
</div>

<!-- details -->

- 领导三人团队（1硕士、2本科），使用强化学习方法设计无人机自主区域防守拦截算法。该算法仅依赖对入侵无人机的无线电到达角测量，实时规划防守无人机的最优任务分配与飞行轨迹，实现无人机的自主集群防守与拦截。
- 提出一种基于MADDPG（多智能体深度确定性策略梯度）的非法入侵无人机主动定位与位置估计策略。在假设防守无人机搭载小型机载雷达的条件下，训练最优拦截路径，最大化雷达测速与定位精度，提升拦截成功率。参考学术成果：“Investigating Multi-UAV Territory Guarding Using Cooperative-Competitive Reinforcement Learning”（AIAA SciTech 2026）。
- 在上述文献的基础上，提出一种基于HA-RMAPPO的无人机集群区域防御改进强化学习方案，利用入侵无人机的无线电回传信号测量，实现对非法入侵无人机位置的被动滤波与定位。该方案适用于小型低成本无人机集群对入侵无人机的快速定位与拦截。
- 在传统HA-RMAPPO的基础上，提出一种基于RNN的训练框架，相比于MLP架构，在定位拦截问题的训练过程中提升了最终拦截策略的成功率。最终成果发表于中科院1区顶级期刊Science China Technological Sciences：“Hybrid reinforcement learning control for UAV territory guarding with cooperative angle-of-arrival localization”（2026）。

<!-- end details -->

## 挑战

- **智能体众多、信息不完整。** 防守无人机集群需要保护指定区域免受敏捷的第一人称视角（FPV）入侵无人机攻击。防守方只能通过被动的无线电到达角（AoA）测量感知入侵者，没有距离信息，因此规划策略必须基于不完整且含噪声的信息做出决策。
- **协同策略难以人工设计。** 实时决定由哪架防守无人机负责定位、哪架负责拦截每个入侵者，是一个困难的协同规划问题。

## 基于强化学习的集群智能

强化学习可作为规划方案生成器：训练完成后，策略能够实时给出决策，并能应对信息不完整和环境复杂的情况。HA-RMAPPO框架（Science China Technological Sciences，2026）包含五个部分：

- **由方位角构建置信。** 集中式粒子滤波器（CPF）融合噪声随距离增大的AoA测量，得到每个入侵者位置的置信分布及3σ置信椭圆。
- **混合动作。** 每架防守无人机输出一个离散的任务分配（感知或拦截哪个入侵者）和一个连续的平面速度指令。
- **威胁触发切换。** 根据置信椭圆最早进入保护区的时间定义概率威胁评分，触发团队从降低不确定性切换到快速拦截。
- **循环网络CTDE训练。** 基于GRU的Actor网络与集中式Critic在集中训练、分散执行框架下用PPO训练，在128个并行环境中共训练10⁷个环境步。
- **两阶段课程学习。** 第一阶段利用入侵者真实状态学习协同；第二阶段在部分可观测条件下基于CPF置信进行微调。

## 结果

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/cuas-rollouts-2v1.png" alt="两架防守无人机对一架入侵无人机的HA-RMAPPO仿真" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">两架防守无人机对一架入侵无人机。(a) 第一阶段，利用真实状态训练。(b) 第二阶段，基于AoA测量构建的CPF置信（灰色为置信椭圆）决策，并进行威胁评估与阶段切换。</div>

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/cuas-comparison-7v3.png" alt="HA-RMAPPO、MAPPO与IPPO训练对比" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">七架防守无人机对三架入侵无人机的第二阶段训练：(a) 防守成功率；(b) 置信协方差的平均对数行列式。对比算法为HA-RMAPPO、MAPPO与IPPO。</div>

训练10⁷步后的最终防守成功率（第二阶段，取最后100个回合的平均值）：

| 防守方 v 入侵方 | HA-RMAPPO（本文） | MAPPO | IPPO  |
| --------------- | ----------------- | ----- | ----- |
| 2v1             | **0.703**         | 0.121 | 0.232 |
| 5v2             | **0.911**         | 0.608 | 0.648 |
| 7v3             | **0.770**         | 0.185 | 0.081 |
