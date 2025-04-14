# Elderly Movement Classification using LSTM

This repository contains the code and methodology for an LSTM-based elderly movement classification system that recognizes 11 activity types from 3D motion data. The system aims to improve elderly safety through non-intrusive, privacy-respecting monitoring.

## Motivation

With a growing elderly population, timely detection of falls or inactivity is critical. Traditional solutions (manual check-ins, cameras, emergency buttons) are limited by privacy issues, user dependence, or scalability. Our approach leverages deep learning with IMU-based sensor data for real-time posture recognition.

## Dataset

- Source: [Kaggle - Posture Reconstruction Dataset](https://www.kaggle.com/datasets/uciml/posture-reconstruction)
- Data: 3D coordinates (X, Y, Z) from 4 skeletal points, time-stamped

## Preprocessing Pipeline

1. **Synchronization**: Align sensor streams using timestamp interpolation
2. **Cleaning & Sorting**: Organize by person ID and chronological order
3. **Normalization**: Standardize data for stable training
4. **Windowing**: Sliding window (size = 30, stride = 1) for augmentation
5. **Split**: Person-independent 80/20 train/test split

Final training set: 30,000+ samples.

## Model Architecture

- 3 LSTM Layers: 128 → 64 → 32 units
- 2 Dense Layers + Softmax output
- Activation: LeakyReLU
- Dropout: 0.3
- Optimizer: Adam (initial LR = 0.01, decay schedule)
- Early Stopping: Patience = 5
- Batch Size: 32, Epochs: 50

## Baseline

- Gated Recurrent Unit (GRU) model
- GRU Accuracy: 92.63%
- LSTM Accuracy: **95.63%**

## Ablation Study

- Learning rate significantly impacts convergence
- LR = 0.1 → failure to converge

## Results

| Model | Accuracy |
|-------|----------|
| LSTM  | 95.63%   |
| GRU   | 92.63%   |

## Contributors

- Yunqing Zhao (yzhao73@uw.edu)  
- Shangming Zhuo (oiviauw@uw.edu)  
*Equal contribution.*

## Limitations

- Fixed context window; dynamic context may be more effective
- Real-world use may require more detailed sensors and better edge hardware

## References

- Lin et al., Sensors, 2023
- Yu et al., Frontiers in Aging Neuroscience, 2021
- Cho et al., arXiv, 2014
- Hochreiter & Schmidhuber, Neural Computation, 1997
