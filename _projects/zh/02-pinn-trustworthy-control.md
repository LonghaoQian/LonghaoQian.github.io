---
layout: page
title: "基于物理信息神经网络（PINN）的可信AI控制框架"
description: "无需训练数据集、严格满足稳定性理论要求的PINN控制网络；结合黎曼流形与收缩分析的鲁棒控制收缩度量（RCCM）。成果已被CDC 2026与AIAA 2027 SciTech Forum录用。"
lang: zh-CN
permalink: /zh/projects/pinn-trustworthy-control/
category: 科研项目
featured: true # shown on the home page
importance: 2
cv_group: utias-postdoc
period: "2025/08至2026/03"
---

**时间：** 2025/08至2026/03 · 多伦多大学航空航天研究院

<!-- details -->

- 领导两人团队（1博士、1硕士），提出一种基于物理信息神经网络（Physics-Informed Neural Networks，PINNs）的非线性控制训练方法，使神经网络能够在完全没有训练数据集的情况下，根据系统的多体动力学方程自动生成鲁棒控制算法，实现复杂系统控制方案的快速生成。相比于传统的机器学习控制，PINN生成的控制方法严格满足控制稳定性的理论要求，实现了基于神经网络的可靠控制方案。
- 通过微分几何，将PINN与黎曼流形理论相结合，实现了对无人机及机器人空间姿态的无奇异控制。结合收缩分析（Contraction Analysis）控制理论，将鲁棒控制问题转化为偏微分方程求解问题，进而使用PINN求解偏微分方程，实现具备稳定性保证的控制网络。
- 首次提出将PINN与黎曼流形相结合的鲁棒控制理论（鲁棒控制收缩度量，Robust Control Contraction Metrics，RCCM），在系统存在外界未知扰动和参数不确定的情况下，仍能保证控制精度。
- 本研究提出的基于PINN的AI控制框架可广泛应用于无人系统控制和具身智能控制中。
- 成果已被国际控制领域顶级会议IEEE Conference on Decision and Control（CDC 2026）和AIAA 2027 SciTech Forum录用，参考学术成果：“Neural Robust Control on Lie Groups Using Contraction Methods”（CDC 2026）、“Contraction-based Neural Control for Cooperative Aerial Payload Transportation with Variable-length Cables”（AIAA 2027 SciTech Forum）。
