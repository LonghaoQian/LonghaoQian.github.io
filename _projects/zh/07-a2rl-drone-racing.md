---
layout: page
title: "2025 A2RL阿布扎比无人机自主飞行竞速比赛"
description: "多伦多大学参赛队无人机控制系统和视觉导航分系统负责人：纯单目视觉竞速，22支队伍中获团体第7名，获得1万美元奖金；8–12 m/s高速飞行跟踪精度约15 cm。"
lang: zh-CN
permalink: /zh/research/a2rl-drone-racing/
category: 竞赛
featured: true # shown on the home page
importance: 7
cv_group: utias-postdoc
period: "2024/09至2025/04"
img: assets/img/projects/a2rl-race-drone.jpg
card_video: assets/video/a2rl-race-flight-card.mp4 # home-page card only
card_video_poster: assets/img/projects/a2rl-race-flight-card-poster.jpg
---

**时间：** 2024/09至2025/04 · 多伦多大学航空航天研究院

**比赛官网：** [a2rl.io/autonomous-drone-race](https://a2rl.io/autonomous-drone-race)

<div class="row mt-3">
  <div class="col-sm mt-3 mt-md-0">
    <figure>
      <video
        src="{{ 'assets/video/a2rl-race-flight.mp4' | relative_url }}"
        poster="{{ 'assets/img/projects/a2rl-race-flight-poster.jpg' | relative_url }}"
        class="img-fluid rounded z-depth-1"
        autoplay
        loop
        muted
        playsinline
      ></video>
    </figure>
  </div>
</div>
<div class="caption">A2RL 2025阿布扎比比赛场地内的一次竞速飞行（隔着安全网拍摄）。</div>

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/a2rl-final-standings.jpg" alt="A2RL 2025最终排名" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">最终排名（22支队伍中的前8名）。多伦多大学代表队UTADR获第7名。</div>

<div class="row">
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/a2rl-longhao-with-drone.jpg" alt="潜龙昊在A2RL比赛场地手持竞速无人机" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/a2rl-race-drone.jpg" alt="A2RL竞速无人机" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">左：潜龙昊在A2RL比赛场地。右：比赛现场的A2RL竞速无人机。</div>

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    <figure>
      <video
        src="{{ 'assets/video/a2rl-practice-flight.mp4' | relative_url }}"
        poster="{{ 'assets/img/projects/a2rl-practice-flight-poster.jpg' | relative_url }}"
        class="img-fluid rounded z-depth-1"
        autoplay
        loop
        muted
        playsinline
      ></video>
    </figure>
  </div>
  <div class="col-sm mt-3 mt-md-0">
    <figure>
      <video
        src="{{ 'assets/video/a2rl-isaac-gsplat.mp4' | relative_url }}"
        poster="{{ 'assets/img/projects/a2rl-isaac-gsplat-poster.jpg' | relative_url }}"
        class="img-fluid rounded z-depth-1"
        autoplay
        loop
        muted
        playsinline
      ></video>
    </figure>
  </div>
</div>
<div class="caption">左：在训练场地的试飞。右：同一场地在Isaac Sim中的3D高斯泼溅（3DGS）重建模型——仿真机载相机画面与场景中的无人机。</div>

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/a2rl-vision-pipeline.png" alt="纯视觉导航流程：训练与实现" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
  纯视觉导航流程。训练：利用比赛场地的3DGS重建模型生成门框角点数据集，训练YOLOv11。机载实现：门框角点检测（10 Hz）→ PnP解算绝对位置 → EKF融合VIO（20–30 Hz）与IMU → 100 Hz MPC控制。
</div>

<!-- details -->

- 代表多伦多大学参加2025 A2RL（Abu Dhabi Autonomous Racing League）无人机自主竞速比赛，担任无人机控制系统和视觉导航分系统负责人。比赛要求仅使用单目相机，在纯视觉定位与导航的前提下完成竞速飞行。
- 作为首次参赛的团队与专业团队同场竞技，取得团体第7名（共22支队伍参赛），获得1万美元奖金。
- 构建数据驱动的竞速无人机高精度动力学模型。应用该模型后，模型预测控制（Model Predictive Control，MPC）的跟踪误差降低20%；在8–12 m/s的高速飞行过程中，无人机跟踪精度可保持在15 cm左右。
- 参与实现了基于三维高斯泼溅（3D Gaussian Splatting，3DGS）技术的视觉导航数据集生成系统。利用3DGS构建飞行场景的三维模型，结合特征点的几何位置，快速生成高精度视觉导航YOLO训练集。
- 与团队协作，实现了基于视觉里程计、IMU和障碍物特征定位的纯视觉动态飞行定位系统，定位精度约为0.2–0.5 m。在比赛中完成了所有规定飞行科目（22支参赛队伍中，仅有8队完成全部飞行科目）。
