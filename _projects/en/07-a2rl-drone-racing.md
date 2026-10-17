---
layout: page
title: "2025 A2RL Abu Dhabi Autonomous Drone Racing"
description: "Lead of the control and visual-navigation subsystems for the University of Toronto team: monocular-camera-only racing, 7th of 22 teams and a US$10,000 prize; ~15 cm tracking accuracy at 8–12 m/s."
lang: en
permalink: /research/a2rl-drone-racing/
category: competition
featured: true # shown on the home page
importance: 7
cv_group: utias-postdoc
period: "2024/09 – 2025/04"
img: assets/img/projects/a2rl-race-drone.jpg
card_video: assets/video/a2rl-race-flight-card.mp4 # home-page card only
card_video_poster: assets/img/projects/a2rl-race-flight-card-poster.jpg
---

**Period:** 2024/09 – 2025/04 · University of Toronto Institute for Aerospace Studies

**Competition website:** [a2rl.io/autonomous-drone-race](https://a2rl.io/autonomous-drone-race)

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
<div class="caption">A race flight in the A2RL 2025 arena in Abu Dhabi, filmed from behind the safety net.</div>

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/a2rl-final-standings.jpg" alt="A2RL 2025 final standings" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">Final standings (top 8 of 22 teams). The University of Toronto team, UTADR, placed 7th.</div>

<div class="row">
  <div class="col-sm-4 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/a2rl-longhao-with-drone.jpg" alt="Longhao Qian holding a race drone at the A2RL venue" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-sm-8 mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/a2rl-race-drone.jpg" alt="A2RL race drone" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">Left: Longhao Qian at the A2RL venue. Right: the A2RL race drone at the racing site.</div>

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
<div class="caption">
  Left: a test flight at the practice venue. Right: the same venue as a 3D Gaussian Splatting (3DGS) reconstruction in Isaac Sim, showing the simulated
  onboard camera view and the drone in the scene.
</div>

<div class="row">
  <div class="col-sm mt-3 mt-md-0">
    {% include figure.liquid path="assets/img/projects/a2rl-vision-pipeline.png" alt="Vision navigation pipeline: training and implementation" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
  Vision-only navigation pipeline. Training: a 3DGS reconstruction of the racing site generates the gate-corner dataset for YOLOv11. Onboard: gate-corner
  detection (10 Hz) → PnP for absolute position → EKF fusing VIO (20–30 Hz) and IMU → MPC at 100 Hz.
</div>

<!-- details -->

- Represented the University of Toronto in the 2025 A2RL (Abu Dhabi Autonomous Racing League) autonomous drone racing competition, serving as lead of the drone control system and the visual-navigation subsystem. The competition required racing flight using only a monocular camera, with purely vision-based localization and navigation.
- As a first-time team competing alongside professional teams, placed 7th overall (out of 22 teams) and won a US$10,000 prize.
- Built a data-driven, high-fidelity dynamics model of the racing drone. With this model, the tracking error of model predictive control (MPC) was reduced by 20%; during high-speed flight at 8–12 m/s, the drone's tracking accuracy was maintained at about 15 cm.
- Contributed to a visual-navigation dataset generation system based on 3D Gaussian Splatting (3DGS). Used 3DGS to build 3D models of the flight scene and, combined with the geometric positions of feature points, rapidly generated high-accuracy YOLO training sets for visual navigation.
- Worked with the team to implement a purely vision-based dynamic flight localization system based on visual odometry, the IMU, and obstacle-feature localization, with a localization accuracy of about 0.2–0.5 m. Completed all required flight tasks in the competition (only 8 of the 22 participating teams completed all flight tasks).
