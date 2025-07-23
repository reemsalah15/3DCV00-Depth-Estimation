# Depth Estimation on CARLA Dataset

This repository provides an implementation, analysis, and comparison of **Monocular** and **Stereo** depth estimation methods on the **CARLA Simulator** dataset.

---

## Models Used

### 1. Monocular Depth Estimation
- **Model:** Depth-Anything-V2 (ViT-Large)
- **Input:** Single RGB image
- **Output:** Depth map (flipped & normalized)
- **Use Case:** Lightweight, works with a single camera.

### 2. Stereo Depth Estimation
- **Model:** RAFT-Stereo (SceneFlow Pre-trained)
- **Input:** Left and Right stereo image pairs
- **Output:** Disparity map (normalized)
- **Use Case:** High accuracy where stereo cameras are available.

---

## Quantitative Results

| Method      | MAE ↓ | RMSE ↓ | AbsRel ↓ | EPE ↓ | Bad-1 ↓ |
|-------------|-------|--------|----------|-------|---------|
| Monocular   | **0.38** | 0.46   | 0.27     |   -   |   -     |
| Stereo      | 0.31  | **0.42**   |   -      | **1.85**  | **12.3%** |

 **Stereo performs better in overall accuracy**, but **Monocular** is more lightweight and suitable for single-camera setups.

---

## Qualitative Examples

### Monocular
![Mono Best](./monocular/outputs/best_example.png)  
![Mono Worst](./monocular/outputs/worst_example.png)

### Stereo
![Stereo Best](./stereo/outputs/best_example.png)  
![Stereo Worst](./stereo/outputs/worst_example.png)

---

##  Discussion

### Strengths
- **Monocular:**
  - Lightweight, single-image input.
  - Works even without stereo hardware.
- **Stereo:**
  - More geometrically consistent.
  - Better performance in textured regions.

### Weaknesses
- **Monocular:** Relies heavily on learned priors, struggles in unseen environments.
- **Stereo:** Struggles with occlusions, reflective/textureless surfaces.

### Failure Cases
- Monocular fails in far-distance objects.
- Stereo fails in repetitive textures and occluded regions.

### Potential Improvements
- Fine-tune both methods on CARLA-like domains.
- Combine monocular priors with stereo matching.
- Apply post-processing (left-right consistency checks).

---

##  Folder Structure

- **`/monocular`** → Monocular notebook, requirements, and outputs.
- **`/stereo`** → Stereo notebook, requirements, and outputs.

Check individual READMEs for detailed instructions.

```
3DCV00-Depth-Estimation/
│
├── monocular/
│   ├── README.md                   # Introduction, results, and instructions for running the monocular method
│   ├── mono_notebook.ipynb         # Jupyter Notebook: inference, metrics calculation, and visualizations
│   ├── requirements.txt            # Required Python packages for the monocular method
│   └── outputs/                    # Output images (Best, Worst, Error Maps, Sample visualizations)
│       ├── best_example.png
│       ├── worst_example.png
│       └── histogram.png
│
├── stereo/
│   ├── README.md                   # Introduction, results, and instructions for running the stereo method
│   ├── stereo_notebook.ipynb       # Jupyter Notebook: inference, metrics calculation, and visualizations
│   ├── requirements.txt            # Required Python packages for the stereo method
│   └── outputs/                    # Output images (Best, Worst, Error Maps, Sample visualizations)
│       ├── best_example.png
│       ├── worst_example.png
│       └── histogram.png
│
└── README.md                       # Main report comparing Monocular and Stereo (intro, results, discussion)
```
