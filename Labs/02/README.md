# Medical Imaging Analysis Portfolio — Lab 02

Lab 02 for Medical Computer Vision: enhancement, multi-modal fusion, and real-time video processing pipelines for clinical diagnostic imaging.

Medical images often come with underexposure, poor tissue contrast, modality-specific strengths and weaknesses, and heavy speckle/backscatter noise. This lab works with real clinical data across three tasks to mathematically and visually enhance diagnostic clarity.

---

## Repository Architecture

```
02/
├── Task_1_Chest_XRay/
│   ├── data/                   # Input X-ray data (COVID.png)
│   ├── output/                 # 8 visual outputs, including the comparison dashboard
│   ├── xray_enhancement.ipynb  # Interactive Jupyter processing notebook
│   └── README.md               # Explanation of the 7-stage enhancement pipeline
│
├── Task_2_Cardiac_Fusion/
│   ├── data/                   # Input CT & MRI slice pairs (slice_001_ct.png, slice_001_mri.png)
│   ├── output/                 # 6 fusion figures, including the comparative dashboard
│   ├── modal_fusion.ipynb      # Interactive Jupyter notebook for multi-modal blending
│   └── README.md               # Explanation of the fusion pipeline & output files
│
├── Task_3_Echo_Analysis/
│   ├── data/                   # Input ultrasound video (0X100F044876B98F90.mp4)
│   ├── output/                 # Frame comparisons, monitoring grid & real-time loop screenshots
│   ├── realtime_echo.ipynb     # Per-frame ultrasound processing pipeline
│   └── README.md               # Instructions & breakdown of the real-time video loop
│
├── requirements.txt            # Global Python library dependencies
└── README.md                   # Main repository overview & setup instructions
```

---

## Tasks Summary

### Task 1: Diagnostic Enhancement of Chest X-Rays (`Task_1_Chest_XRay/`)
- **Focus:** Maximizing structural and pathology visibility in an underexposed chest X-ray (`COVID.png`).
- **Techniques:** Histogram equalization, `COLORMAP_JET` false-color heatmaps, per-channel color balancing, binary high-intensity thresholding (dense tissue mask), logarithmic expansion, and fractional power-law (gamma $\gamma=0.5$) midtone brightening.

### Task 2: Multi-Modal Cardiac Image Fusion (`Task_2_Cardiac_Fusion/`)
- **Focus:** Blending matched CT (`slice_001_ct.png`) and MRI (`slice_001_mri.png`) cardiac slices into one composite.
- **Techniques:** Independent histogram equalization, complementary false-color mapping (`COLORMAP_BONE` for CT, `COLORMAP_HOT` for MRI), weighted linear blending ($\alpha=0.65$ CT for structural accuracy, $\beta=0.35$ MRI for soft-tissue detail), and log/gamma post-processing.

### Task 3: Real-Time Echocardiogram Video Analysis (`Task_3_Echo_Analysis/`)
- **Focus:** Real-time per-frame enhancement of a noisy cardiac ultrasound video (`0X100F044876B98F90.mp4`).
- **Techniques:** Frame-by-frame OpenCV pipeline (contrast restoration, blood-flow pseudocoloring, logarithmic dark-chamber expansion, gamma-based speckle suppression at $\gamma=1.4$), a side-by-side monitoring array, and a continuous `while`-loop pass over the full video with a live/headless-safe display.

---

## Quick Start & Setup

### 1. Install Dependencies
Requires Python 3.8+.

```bash
pip install -r requirements.txt
```

### 2. Run the Notebooks
```bash
jupyter notebook
```

Open the notebook for the task you want:
- Task 1: `Task_1_Chest_XRay/xray_enhancement.ipynb`
- Task 2: `Task_2_Cardiac_Fusion/modal_fusion.ipynb`
- Task 3: `Task_3_Echo_Analysis/realtime_echo.ipynb`

Running all cells populates that task's `output/` folder with the corresponding visual results.

---

*Documentation in this repository was prepared with the help of AI.*