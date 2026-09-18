# 🚶 Pedestrian Intent Forecaster

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white)
![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=for-the-badge)

A predictive computer vision pipeline designed for autonomous vehicles and ADAS. By analyzing sequential video frames from an ego-vehicle's dashcam, this system models the spatio-temporal dynamics of pedestrians to forecast their immediate future actions (e.g., crossing vs. not crossing) and estimate their continuous future trajectories. 

---

## ✨ Key Features

* **Crossing Intent Classification:** Predicts the binary probability of a pedestrian stepping into the roadway within the next 1–3 seconds, allowing for proactive vehicle deceleration.
* **Trajectory Forecasting:** Generates continuous 2D coordinates representing the pedestrian's anticipated path over a future time horizon.
* **Spatio-Temporal Modeling:** Utilizes sequence models (`[e.g., Spatio-Temporal Graph Convolutional Networks (ST-GCN) or Transformer-based encoders]`) to capture complex human kinematics and environmental context.
* **Context-Aware Processing:** Integrates bounding box coordinates, ego-vehicle speed, and estimated human pose (keypoints) to refine behavioral predictions.
* **Real-Time Inference Capability:** Optimized for low-latency edge deployment, ensuring predictions are generated fast enough for critical braking systems.

---

## 🏗️ Pipeline Architecture

```text
                      +-------------------------+
                      | Ego-Vehicle Video Feed  |
                      +------------+------------+
                                   |
                                   v
                      +-------------------------+
                      | Object Detection & Pose |
                      | (Bounding Boxes/Joints) |
                      +------------+------------+
                                   |
                                   v
+------------------+  +-------------------------+
| Ego-Vehicle      |->| Spatio-Temporal Encoder | (RNN / LSTM / Transformer)
| Speed/Odometry   |  | (Sequence Modeling)     |
+------------------+  +------------+------------+
                                   |
                +------------------+------------------+
                |                                     |
                v                                     v
      +-------------------+                 +-------------------+
      | Intent Classifier |                 | Trajectory Regressor|
      | (Crossing: 88%)   |                 | (Future X, Y Paths) |
      +-------------------+                 +-------------------+
