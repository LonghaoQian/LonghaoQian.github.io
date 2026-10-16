---
layout: page
title: "Ph.D. Research: Cooperative Tethered-Payload Transportation with Multiple Drones"
description: "Lyapunov-based nonlinear control for multi-drone tethered-payload transport (JGCD, IEEE TIE, IEEE/ASME TMECH; 300+ citations), implemented from scratch in C++/ROS on a Jetson Nano with a Pixhawk."
lang: en
permalink: /research/phd-cooperative-payload-transport/
category: research
importance: 8
cv_group: utias-phd
period: "2016/09 – 2021/03"
---

**Period:** 2016/09 – 2021/03 · Ph.D., University of Toronto Institute for Aerospace Studies · Supervisor: Dr. Hugh H.T. Liu

<!-- details -->

- Conducted research on the control theory and engineering implementation of autonomous drone transportation systems. For applications in which multiple drones carry a tethered payload, proposed a complete set of nonlinear control methods based on multibody dynamics, achieved cooperative payload transportation with multiple drones, and built an experimental platform to validate the engineering feasibility of the approach, providing a solution to the control challenges of cooperative drone transportation in future smart cities.
- The project was jointly funded by the Natural Sciences and Engineering Research Council of Canada (NSERC) and Drone Delivery Canada, with total funding of C$640,000 (approx. RMB 3.2 million).
- The outstanding doctoral research was supported by full scholarships from the University of Toronto and the Government of Ontario: the Ontario Trillium Scholarship (awarded to only 75 recipients across Ontario), totaling C$160,000 (approx. RMB 820,000).
- On the theoretical side, proposed a nonlinear control system based on the Lyapunov method and proved that it guarantees stable transportation of the tethered payload in the presence of unknown disturbances, providing a technical foundation for safe payload transportation in adverse weather. The results were published in the top international journals Journal of Guidance, Control, and Dynamics (top aerospace journal, CAS JCR Zone 1), IEEE Transactions on Industrial Electronics (top mechatronics and automation journal, CAS Zone 1), and IEEE/ASME Transactions on Mechatronics (top mechatronics and automation journal, CAS Zone 1). The related work has received more than 300 citations and wide recognition in the academic community ([Google Scholar](https://scholar.google.ca/citations?hl=en&user=p2oGLVYAAAAJ)).
- On the engineering side, independently implemented the nonlinear control methods for multi-drone cooperative transportation from scratch. Wrote the flight control programs in C++ and ROS, and implemented the real-time flight control algorithms, as well as command control of the Pixhawk flight control computer, on the resource-constrained NVIDIA Jetson Nano onboard computer, providing a practical software solution for engineering deployment; validated the correctness and fault-tolerant control capability of the proposed methods on quadrotor drones.
- Project video and GitHub repository:
  - YouTube: <https://www.youtube.com/watch?v=ejTnwAZaz20>
  - GitHub: <https://github.com/LonghaoQian/px4_command>
