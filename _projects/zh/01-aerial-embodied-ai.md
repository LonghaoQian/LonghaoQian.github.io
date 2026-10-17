---
layout: page
title: "基于无人机机械臂平台的空中具身智能与视觉语言大模型（VLM）研究"
description: "基于L1自适应控制的空中机械臂操作（平均误差3–4 cm）、PPO Sim2Real控制校正、Jetson Orin 400 Hz直接控制，以及基于Qwen2.5-VL的自主识别与抓取。"
lang: zh-CN
permalink: /zh/research/aerial-embodied-ai/
category: 科研项目
featured: true # shown on the home page
importance: 1
cv_group: utias-postdoc
period: "2025/10至今"
img: assets/img/projects/arm-isaac-thumb.jpg
card_img: assets/img/projects/arm-isaac-model.jpg # home-page card only
card_video: assets/video/arm-flight-card.mp4 # home-page card only
card_video_poster: assets/img/projects/arm-flight-card-poster.jpg
---

**时间：** 2025/10至今 · 多伦多大学航空航天研究院

<blockquote class="block-tip">
  <p>
    <strong>项目进行中。</strong>我们在空中操作方面已取得显著进展。基于视觉的物体定位与大模型控制均已完成测试，目前正在开展实验，缩小与飞行中全自主抓取之间的剩余差距。
  </p>
</blockquote>

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
    <figure>
      <video
        src="{{ 'assets/video/arm-flight.mp4' | relative_url }}"
        poster="{{ 'assets/img/projects/arm-flight-poster.jpg' | relative_url }}"
        class="img-fluid rounded z-depth-1"
        autoplay
        loop
        muted
        playsinline
      ></video>
    </figure>
  </div>
</div>
<div class="caption">飞行实验：无人机机械臂平台在室内飞行场地中展开机械臂与夹爪飞行。</div>

<!-- details -->

- 领导四人团队（3博士、1硕士），设计无人机机械臂平台的交互抓取与轨迹跟踪算法。本人负责L1自适应控制算法设计、机械臂调试与校准，以及系统总体架构设计（通信链路与软件系统）。通过分析机械臂平台的多体动力学方程，提出基于L1自适应控制的空中具身智能框架，填补了空中智能机械臂平台稳定性理论证明的空白。在飞行实验中实现了3–4 cm的平均动态物体操作误差，达到现有文献中空中串联机械臂物体操作的最高精度。基于通义千问Qwen2.5-VL-7B实现空中具身平台的VLM功能，使平台能够自主识别目标物，并调用底层视觉定位算法完成抓取前定位；基于Qwen2.5-7B实现对无人机的自然语言控制。
- 针对飞行系统中的参数不确定性，例如空气阻力、螺旋桨下洗气流（旋翼产生的向下气流）对飞行的影响，采用近端策略优化（Proximal Policy Optimization，PPO）强化学习方法结合域随机化（Domain Randomization），缩小Sim2Real（仿真到真实环境迁移）差距。在NVIDIA Isaac Sim 6.0和Isaac Lab 3.0中训练PPO控制校正算法。
- 在NVIDIA Jetson Orin机载电脑上部署具身智能控制框架，通过以太网实现机载电脑与飞行控制单元之间基于UDP的高速低延迟通信。首次实现由NVIDIA Jetson Orin以400 Hz的频率直接控制无人机螺旋桨和机械臂，大幅提升了操作与跟踪精度。
- 采用XM430-W350关节作动器，设计FOC（磁场定向控制）电流环控制，在力矩控制模式下将力矩作动精度提升约20%，为整体物体操作精度的提升打下基础。
- 使用RealSense深度相机，利用Ultralytics运行YOLOv8，结合RGB物体检测与深度信息，实现目标的自主识别与定位，对静态目标的定位精度达到厘米级。
- 在配备RTX 4070的地面站电脑上本地部署通义千问Qwen2.5-VL-7B大模型，无人机通过P2P网络连接地面控制站，实时获取无人机和机械臂的运动状态。大模型通过识别相机图像中的物体，调用RealSense深度相机模块的精确定位结果，实现空中具身平台的全自主环境交互系统。大模型调用本研究提出的具身控制框架，控制无人机完成物体的抓取和放置，实现了以大模型为核心的物理AI闭环专家系统。

<!-- end details -->

## 基于Isaac Sim的Sim2Real

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/arm-sim2real-framework.jpg" alt="Sim2Real迭代框架" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">Sim2Real迭代闭环：实测数据、高保真仿真、并行强化学习训练、飞行实验，再回到实测数据。</div>

1. **实测数据。** 在测试台上测量电机转速与推力，并拟合其与油门的关系；结合CAD模型确定仿真参数。
2. **高保真仿真。** 将CAD设计从Onshape导出为USD文件并导入基于PhysX引擎的NVIDIA Isaac Sim。通过ROS 2接口读取真值并设置关节力矩，使同一套控制代码既能在仿真中运行，也能在实机上运行。
3. **并行强化学习训练。** 在Isaac Lab中利用大量并行环境训练PPO控制校正策略，并对空气阻力、旋翼下洗气流等难以建模的因素进行领域随机化，缩小Sim2Real差距。
4. **实验验证。** 控制器与策略在实机平台上飞行验证，飞行数据进入下一轮迭代。

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/arm-isaac-model.jpg" alt="Isaac Sim中的无人机机械臂模型" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/arm-hardware.jpg" alt="无人机机械臂实物" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">同一无人机机械臂平台在Isaac Sim中的模型（左）与实物（右），机身下方为Intel RealSense D435i深度相机与机械臂。</div>

<div class="row">
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/arm-test-stand.jpg" alt="电机与螺旋桨测试台" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm-8 mt-3 mt-md-0 d-flex align-items-center">
    {% include figure.liquid path="assets/img/projects/arm-thrust-curves.png" alt="电机转速与推力随油门变化的实测曲线" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">测试台实测的电机转速与推力随油门变化曲线，用于标定仿真模型。</div>

<div class="row">
  <div class="col-sm-8 mx-auto mt-3 mt-md-0">
    <figure>
      <video
        src="{{ 'assets/video/arm-isaac-takeoff.mp4' | relative_url }}"
        poster="{{ 'assets/img/projects/arm-isaac-takeoff-poster.jpg' | relative_url }}"
        class="img-fluid rounded z-depth-1"
        autoplay
        loop
        muted
        playsinline
      ></video>
    </figure>
  </div>
</div>
<div class="caption">Isaac Sim：无人机机械臂平台起飞仿真，包含与地面的接触。</div>

## 飞行实验

页面顶部的视频展示了平台在室内飞行场地中的飞行。实验中的主要结果：

- **平均动态操作误差3–4 cm**：基于L1自适应控制框架。
- **NVIDIA Jetson Orin以400 Hz直接控制**：通过以太网低延迟UDP通信连接飞控单元，直接控制旋翼与机械臂。
- **力矩控制精度提升约20%**：对XM430-W350关节执行器设计FOC（磁场定向控制）电流环控制。
- **静态目标厘米级定位**：基于RealSense深度相机与YOLOv8。

## 大模型（LLM/VLM）闭环

<style>
  .llm-flow {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: center;
    gap: 0.5rem;
    margin: 1rem 0;
  }
  .llm-flow > div {
    border: 1px solid rgba(127, 127, 127, 0.45);
    border-radius: 0.5rem;
    padding: 0.5rem 0.75rem;
    text-align: center;
    font-size: 0.9rem;
    line-height: 1.35;
  }
  .llm-flow > span {
    opacity: 0.6;
  }
</style>

<div class="llm-flow">
  <div><strong>指令</strong><br>自然语言</div>
  <span>→</span>
  <div><strong>Qwen2.5-7B</strong><br>语言转化为任务</div>
  <span>→</span>
  <div><strong>Qwen2.5-VL-7B</strong><br>在图像中识别目标</div>
  <span>→</span>
  <div><strong>RealSense + YOLOv8</strong><br>目标三维位置</div>
  <span>→</span>
  <div><strong>L1自适应控制</strong><br>Jetson Orin 400 Hz</div>
  <span>→</span>
  <div><strong>抓取与放置</strong></div>
</div>

1. **语言。** 基于Qwen2.5-7B（通义千问）将自然语言指令转化为无人机任务。
2. **视觉。** Qwen2.5-VL-7B在相机图像中识别目标物体。
3. **定位。** RealSense深度相机与YOLOv8给出目标的三维位置，用于抓取前定位。
4. **控制。** 具身控制框架控制无人机与机械臂完成物体的抓取和放置。

Qwen2.5-VL-7B本地部署于配备RTX 4070的地面站电脑上。无人机通过P2P网络与地面站连接，实时传输无人机与机械臂的运动状态，形成以大模型为核心的闭环。

**当前进展。** 基于视觉的物体定位与大模型控制均已完成测试，将二者结合实现飞行中全自主抓取的实验正在进行中。

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    <figure>
      <video
        src="{{ 'assets/video/arm-bottle-localization.mp4' | relative_url }}"
        poster="{{ 'assets/img/projects/arm-bottle-localization-poster.jpg' | relative_url }}"
        class="img-fluid rounded z-depth-1"
        autoplay
        loop
        muted
        playsinline
      ></video>
    </figure>
  </div>
</div>
<div class="caption">飞行中的视觉定位基线（30秒片段）。RealSense相机检测到瓶子（右）；结合动捕系统提供的无人机位姿，通过标定的相机安装参数将检测深度投影到世界坐标系。无人机运动时，运行中位数估计（星号）稳定在固定位置（左）。</div>

## 团队

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/arm-team.jpg" alt="项目团队与无人机机械臂平台在飞行场地合影" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
  项目团队与无人机机械臂平台在飞行场地合影。从左至右：博士生
  <a href="https://flight.utias.utoronto.ca/index.php/enoch-lo">Enoch Lo</a>、
  <a href="https://flight.utias.utoronto.ca/index.php/keilan-pieper">Keilan Pieper</a>、Shiqi Gao，以及潜龙昊。
</div>
