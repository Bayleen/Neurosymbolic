# Robot Intention Classification with Perceiver Transformer

This repository contains the implementation of the **robot intention recognition model** from our paper, where voxelized RGB-D inputs are processed via a Perceiver Transformer to classify fine-grained robotic actions.

## Overview

We propose a voxel-based pipeline that takes RGB-D images of robot demonstrations and outputs one of eight predefined intention classes:

- `reaching`
- `grasping`
- `lifting`
- `holding`
- `transporting`
- `placing`
- `releasing`
- `nothing`

The architecture consists of:

1. **Voxelization Module**: Converts RGB-D frames into voxel grids with RGB + occupancy features.
2. **Perceiver Transformer**: Processes flattened voxel features through cross-attention into latent tokens.
3. **MLP Classifier**: Maps latent tokens to softmax intention predictions.

## Directory Structure

```
robot_intention/
│
├── perceiver_model.py         # Perceiver transformer model implementation
├── train.py                   # Training script
├── utils/
│   ├── voxel_utils.py         # RGB-D to voxel conversion
│   ├── loss_utils.py          # Class-weighted loss
│   └── data_loader.py         # Dataset class
│
├── checkpoints/               # Saved models
├── results/
│   ├── perceiver_loss.png     # Loss curve figure
│   └── perceiver_probs.png    # Softmax probability heatmap
│
└── README.md
```

## Training Details

- Dataset: RH20T (robot demonstrations)
- Input: Voxel grids of shape `(D x H x W x 4)`
- Optimizer: Adam
- Learning rate: `1e-4`
- Batch size: `2`
- Epochs: `100`
- Device: NVIDIA RTX 4070 GPU

## Results

- Final Test Accuracy: **70.00%**
- Strong confidence in `nothing`, `holding`
- Confusion observed in `grasping`, `lifting` due to action similarity

Visualizations of training loss and softmax outputs can be found in the `results/` folder.

## Future Work

We plan to extend this model to use temporal voxel sequences and integrate it with the human branch for joint correspondence learning. See the full paper for discussion.


