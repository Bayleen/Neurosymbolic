# 🤖 Robot Intention Classification – README

This module contains code and data for robot intention classification using voxelized RGB-D inputs and a Perceiver Transformer. It corresponds to the **robot branch** in our ICRA2025 project and complements the human intention module.

---

## 📁 Directory Structure

```bash
ICRA/
├── dataset_depth/
│   ├── human/                         # Human demo data from Jie
│   └── robot/
│       └── cam_104122061850/
│           └── pick/
│               ├── 0004/
│               ├── 0035/
│               ├── 0038/
│               ├── 0044/
│               └── label_dict.json   # Auto-generated label mapping
│
├── Generate_Voxels/
│   ├── __pycache__/                  # Auto-generated
│   ├── checkpoints/
│   │   ├── depth_anything_v2_base/  # Pretrained model folder
│   │   └── DAV2/                     # Pretrained weights
│   ├── get_depth_images.py
│   ├── pcl_voxelization.py
│   ├── utilis.py
│   └── label_dict_robot.py
│
├── Preceiver_model/
│   ├── label_dict.json
│   ├── perceiver_training.py
│   └── perceiver_model.pth          # Saved model after training


```
## 🛠️ Setup Instructions
### Step 1: Create and activate environment
conda create -n icra_robot python=3.10
conda activate icra_robot

### Step 2: Install dependencies
pip install -r requirements.txt  # Or install manually:
pip install torch torchvision open3d opencv-python tqdm


## 🚀 Running the Pipeline
### Step 1: Generate Depth Images from RGB
cd Generate_Voxels
python get_depth_images.py

Generates .png depth maps from RGB images using Depth Anything V2.
Requires pretrained weights under checkpoints/depth_anything_v2_base/.

### Step 2: Voxelize RGB-D Data
python pcl_voxelization.py

Produces voxel .npy files for each robot sequence.
Includes RGB + occupancy information in voxel grid.

### Step 3: Generate Label Dictionary
python label_dict_robot.py

Outputs label_dict.json used for training.

### Step 4: Train the Perceiver Model
cd ../Preceiver_model
python perceiver_training.py

Loads voxel features and labels, trains robot intention classifier.
Output: perceiver_model.pth and console logs with accuracy/loss.



