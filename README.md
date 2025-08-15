# AutoPose  
Pose-Level Synthetic Data Augmentation for Action Recognition (Research Purposes Only)  
=============================================================

#### Licensed under NSCLv2, where users can use this noncommercially (research or evaluation purposes only) on NVIDIA Processors.  
This project will download and install additional third-party open source software projects. Review the license terms of these open source projects before use.

![mmm-gif-autopose](https://github.com/user-attachments/assets/96147078-f22b-4656-9762-c6a90d71ed21)


### [Colab demo redacted for conference submission purposes]  
### [Hugging Face demo redacted for conference submission purposes]


**AutoPose** is an open-source toolkit that generates class-balanced, kinematically valid video clips by automatically **interpolating human poses** rather than rendering full photorealistic frames. The framework addresses dataset imbalance by creating synthetic data for minority action classes in action-recognition datasets without requiring additional sensors or modalities, using only RGB videos.

Each component of the framework can be swapped with models or components of your choice. While the original implementation used an action recognition network for the augmentation optimization loop, users can integrate their preferred models. Components may be used individually or automated for a specific use case.

![pipeline_demo](https://github.com/user-attachments/assets/1fde62ce-67a6-4673-9341-78da4daa31e4)

---

## Why Pose-Level Augmentation?

| Capability                                                | **AutoPose (Pose)**               |
|-----------------------------------------------------------|------------------------------------|
| Fine-grained motion control                               | ✅ Improved on prior works         |
| Independence from textures                                | ✅ Improved on prior works         |
| Maintaining semantic labels and kinematic plausibility    | ✅ Improved on prior works         |

Pose-level synthesis keeps joint semantics explicit, reduces visual artifacts, and allows customizable generation speed and quality on NVIDIA GPUs.  
This code has been developed and tested only with NVIDIA Processors.

## Publications [Redacted for Conference Review]

---

## Repository Structure  
## Minimal Setup Checklist

| Step | Command / Action | Notes |
|------|------------------|-------|
| **1 Install deps** | `pip install -r requirements.txt` | CUDA-enabled PyTorch recommended |
| **2 Clone sub-repos** | `git clone` the five required repos *(see list below)* | Keep the folder names unchanged |
| **3 Create `.env`** | Add your required keys and paths to each repo | No keys provided in this repo |
| **4 Download models** | Obtain all checkpoints from setup instructions | Place files exactly as instructed |
| **5 Smoke-test** | Run each repo’s test script once and then run `components\running.py` | Fail-fast before running the full pipeline |
| **6 Automate Pipeline** | Select your CV model for the optimization loop and automate using included components | Each use case is user-defined |

### Required External Repositories

```text
StridedTransformer-Pose3D/
text-to-motion/
joints2smpl/
SlowFast/
Blender-3.0.0/          (binary drop)
