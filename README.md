# Residual Learning for Improving Autonomous Powder Weighing

MSc Data Science and Artificial Intelligence — University of Liverpool
Digital Innovation Facility | AIchemy Research Hub
Supervisor: Dr Gabriella Pizzuto

---

## Overview

This project extends FLIP (Flowability-Informed Powder Weighing), a 
reinforcement learning framework for autonomous milligram-scale powder 
dispensing using a Franka Research 3 (FR3) robot arm. FLIP achieves a 
mean dispensing error of 2.12 ± 1.53 mg but operates without any visual 
observation of the spatula during dispensing — it cannot detect powder 
clumps, distribution, or quantity on the spatula surface.

This project addresses that limitation by training a vision-conditioned 
residual policy π_R on top of the frozen FLIP base policy π_B:

    π_new = π_B + π_R

The residual policy takes RGB-D observations from an Intel RealSense D405 
camera and the FLIP base action as input, and outputs a corrective 
adjustment in the same continuous action space (shake amplitude and spatula 
inclination angle).

---

## Structure

- **Phase 1 — Visual Module**: Extends the existing colour segmentation 
  module into a structured feature vector using CIELAB segmentation, 
  spatial distribution statistics, and depth-based volume estimates from 
  the RealSense D405.

- **Phase 2 — Residual Policy Training**: SAC-based residual policy trained 
  using RLPD (Reinforcement Learning with Prior Data), seeded with 
  successful FLIP rollouts and refined through online robot interactions.

- **Phase 3 — Deployment and Evaluation**: Combined policy evaluated across 
  seven powders (sand to flour, AoR 28°–51°) at 15 mg and 20 mg target 
  masses, compared against the FLIP curriculum baseline.

---

## Hardware Stack

- Franka Research 3 (FR3) robot arm
- Robotiq 85F gripper
- Intel RealSense D405 RGB-D camera
- Fisherbrand FPRS223 precision scale

---

## Dependencies

- Python 3.x
- PyTorch
- Franky (FR3 robot control)
- Intel RealSense SDK
