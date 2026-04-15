# Transformer-Based Multi-Modal Trajectory Prediction

This project implements a **Transformer-based trajectory prediction model** using the **nuScenes dataset**.

The model predicts the **future positions of pedestrians and cyclists** from past motion.

---

## Model Architecture

Past trajectory (x, y, vx, vy)

↓

Transformer Encoder

↓

Multi-modal trajectory decoder

↓

Predicted future trajectories

---

## Metrics

| Metric | Description |
|------|------|
| ADE | Average Displacement Error |
| FDE | Final Displacement Error |

Example results:

```
ADE ≈ 0.27
FDE ≈ 0.48
```

---

## Visualization

![Trajectory Demo](results/trajectory_demo.gif)

---

## Installation

```
pip install -r requirements.txt
```

---

## Running

Open the notebook:

```
trajectory_prediction.ipynb
```

---

## Author

Trajectory prediction project using deep learning and Transformers.
