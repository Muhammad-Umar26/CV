# Task 2: Multi-Modal Cardiac Image Fusion (CT + MRI)

Fuses a matched CT and MRI slice of the same cardiac cross-section into one composite image carrying CT's structural precision and MRI's soft-tissue richness.

## Dataset

- **CT Slice:** `slice_001_ct.png` — grayscale 8-bit, loaded from `data/slice_001_ct.png`
- **MRI Slice:** `slice_001_mri.png` — grayscale 8-bit, loaded from `data/slice_001_mri.png`

## Pipeline

1. **Raw Modalities** — load and display CT and MRI side-by-side
2. **Histogram Equalization** (`cv2.equalizeHist`) — normalize each modality's dynamic range independently
3. **False-Color Mapping** (`cv2.applyColorMap`) — CT → `COLORMAP_BONE`, MRI → `COLORMAP_HOT`
4. **Weighted Fusion** (`cv2.addWeighted`) — blend $I_{fused} = 0.65 \cdot I_{CT} + 0.35 \cdot I_{MRI}$
5. **Logarithmic Transform** — $s = c \cdot \ln(1 + r)$ on the fused image to recover shadow detail
6. **Gamma Transform** — $s = c \cdot r^{\gamma}$, $\gamma = 0.8$, to balance midtones
7. **Comparison Dashboard** — all 6 stages side-by-side

## Output Files (`output/`)

| File | Stage |
|---|---|
| `01_ct_mri_raw.png` | Raw CT and MRI side-by-side |
| `02_equalized_modalities.png` | Histogram-equalized modalities |
| `03_colored_heatmaps.png` | BONE/HOT false-color heatmaps |
| `04_weighted_fusion.png` | Weighted fusion (0.65·CT + 0.35·MRI) |
| `05_log_and_power_law_fusion.png` | Log- and gamma-transformed fusion |
| `06_comparative_analysis_dashboard.png` | Full pipeline comparison |

## How to Run

1. Open `modal_fusion.ipynb`.
2. Run all cells top to bottom.
3. Outputs are saved to `output/`.