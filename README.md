# Transformer-Based Multi-Modal Trajectory Prediction

This project implements a **Transformer-based trajectory prediction model** using the **nuScenes dataset**.

The model predicts the **future positions of pedestrians and cyclists** from past motion.

---

## Model Architecture

Past Trajectory (2s)
(x, y, vx, vy)

        │
        ▼

Feature Embedding
Linear Projection → 128D

        │
        ▼

Transformer Encoder
(Self-Attention + Feedforward)

        │
        ▼

Context Vector
(Final timestep representation)

        │
        ▼

Multi-Modal Decoder

        │
        ▼

Future Trajectory Predictions
3 possible trajectories
+ probability scores

---

## Detailed Model Architecture

Input: Past Agent Trajectory
--------------------------------
Features per timestep:
(x position, y position, x velocity, y velocity)

Sequence Length: 2 seconds of motion


Step 1 — Feature Embedding
--------------------------------
Each timestep feature vector is projected into a higher-dimensional representation.

Input (4D) → Linear Layer → 128D Embedding


Step 2 — Transformer Encoder
--------------------------------
The embedded sequence is processed using a Transformer encoder to model temporal dependencies.

Components:

• Multi-Head Self-Attention
    Each timestep looks at every other timestep to understand the motion pattern. 
    Instead of looking at the motion in one way, the model looks at it in multiple ways simultaneously.
    So the model can understand different motion patterns at the same time.
    
• Feed-Forward Network
    After attention understands the relationships between timesteps, the result goes through a small neural network.
    Linear Layer:
        → ReLU activation
        → Linear Layer
        
• Layer Normalisation
    Neural networks can become unstable while training.
    Layer Normalisation helps by:
        → keeping the values balanced
        → stabilising training
        → improving learning speed



Output:
Temporal motion representation (new representation of the trajectory sequence which includes movement direction, speed changes, trajectory curvature, motion patterns)



Step 3 — Context Extraction
--------------------------------
The encoder output at the final timestep is used as the trajectory context vector.


Step 4 — Multi-Modal Decoder
--------------------------------
A fully connected decoder predicts multiple possible future trajectories.

Outputs:
• 3 candidate trajectories
• Probability score for each trajectory


Step 5 — Future Trajectory Prediction
--------------------------------
Prediction horizon: 3 seconds

Each predicted trajectory contains:
(x, y) coordinates for each timestep

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

### Research Style Demo
Prediction branches with probability visualization.

<p align="center">
<img src="results/trajectory_research_demo.gif" width="700">
</p>

---

### Video Demo
Full trajectory animation.

[Watch Video](results/trajectory_prediction.mp4)

### Single-Agent Trajectory Prediction
Example prediction with multiple possible futures.

<p align="center">
<img src="results/trajectory_demo.gif" width="700">
</p>

---

### Multi-Agent Scene Prediction
Multiple pedestrians moving simultaneously.

<p align="center">
<img src="results/multi_agent_prediction.gif" width="700">
</p>

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
Shivapuram Samanvitha
GitHub: https://github.com/samanvithashivapuram
