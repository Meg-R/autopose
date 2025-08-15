# AutoPose – Setup Guide [edited for conference submission]
This guide walks you through installing dependencies, placing pretrained models, and testing each component of the AutoPose pipeline. Common errors and fixes are also provided.

---

## 📦 Step 1: Install Dependencies
```bash
pip install -r requirements.txt
```

---

## 📁 Step 2: Clone Required Repositories
Clone the following into your project root:

- [StridedTransformer-Pose3D](https://github.com/Vegetebird/StridedTransformer-Pose3D)
- [text-to-motion](https://github.com/EricGuo5513/text-to-motion)
- [joints2smpl](https://github.com/wangsen1312/joints2smpl)
- [Blender 3.0.0](https://download.blender.org/release/Blender3.0/)
- [SlowFast](https://github.com/facebookresearch/SlowFast)

---

## ⚙️ Step 3: Configuration
Create `.env` in the root with:

- Your OpenAI GPT API key
- Folder paths to each cloned repository

---

## 💾 Step 4: Pretrained Models
Download pretrained checkpoints:  
[Google Drive Link](https://drive.google.com/drive/folders/1E-ZslWCYv07YeGJbQxSFM3GiVt6tKrNk?usp=sharing)  
Follow each repo’s instructions for placement.

---

# Component Setup & Testing

## 🎯 StridedTransformer-Pose3D
Generates Human3.6M 3D pose estimations from real videos.

**Model placement:**
```
./checkpoint/pretrained/        # 2 .pth files
./demo/lib/checkpoint/           # 2 .pth files
```

**Test:**
```bash
python demo/vis.py --video sample_video.mp4
```

**Common Fix:**  
`model_path` errors → ensure video is single continuous action with full body visible.

---

## 🎬 text-to-motion
Generates 3D pose sequences from text.

**Model placement:**
```
./checkpoints/kit/
./checkpoints/t2m/
```

**Test:**
```bash
python gen_motion_script.py --name Comp_v6_KLD01 --text_file input.txt --repeat_time 1
```

**Common Fixes:**
- `np.float` errors → replace with `float` or `np.float64`
- `ax.lines` errors → adjust `update(index)` in `plot_script.py`
- Missing SpaCy model → `python -m spacy download en_core_web_sm`
- Missing ffmpeg → `conda install -c conda-forge ffmpeg`

---

## ⚙️ joints2smpl
Attaches generated joints to SMPL body models.

**Model placement:**
```
./smpl_models/smpl/
```

**Test:**
```bash
python fit_seq.py --files test_motion2.npy
```

**Common Fix:**  
`np.bool` import error → modify `chumpy/__init__.py` to use `bool` or `np.bool_`.

---

## 🎬 Blender
Renders `.ply` objects into video.

**Install Blender 3.0.0:**
```bash
wget https://download.blender.org/release/Blender3.0/blender-3.0.0-linux-x64.tar.xz
tar -xf blender-3.0.0-linux-x64.tar.xz
```

**Setup:**
- Place `animation_pose.py` in Blender directory
- Create `angleInput.txt` with desired camera angle (e.g., `front`)

**Test:**
```bash
./blender -b -P animation_pose.py -- --name <ply_folder>
```
---

## 🚀 Step 5: Running the AutoPose Pipeline
Once all components are set up and tested individually, run the generation-only script by selecting either the **synthetic-mix** or **real-mix** option:

```bash
python components/running.py 
```

Commment out the function you do not want to try out, and fill in the directory as per the `running.py' script. This will execute the full AutoPose pipeline using the chosen configuration.

# 🔧 General Troubleshooting

| Issue | Cause | Fix |
|-------|-------|-----|
| Paths not found | `.env` not read | Hardcode paths or store in Python config file |
| `python` not recognized | Python3 mismatch | `sudo ln -s $(which python3) /usr/local/bin/python` |

