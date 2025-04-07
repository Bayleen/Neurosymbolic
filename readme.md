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
