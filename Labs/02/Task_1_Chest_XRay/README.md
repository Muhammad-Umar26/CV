# Task 1: Diagnostic Enhancement of Chest X-Rays

Enhances an underexposed chest X-ray to make lung structures and dense tissue easier to see.

## Dataset

- **Image:** `covid.png` — grayscale 8-bit (loaded from `data/covid.png`)

## Pipeline

1. **Raw X-Ray** — load baseline grayscale image
2. **Histogram Equalization** (`cv2.equalizeHist`) — spread intensities across 0–255
3. **JET Colormap** (`cv2.COLORMAP_JET`) — map equalized image to a false-color heatmap
4. **Color Balance** — per-channel gains ($R{\times}1.2$, $G{\times}0.95$, $B{\times}0.9$) on the heatmap
5. **Dense Tissue Threshold** — binary threshold ($T \ge 200$) on the equalized image
6. **Logarithmic Transform** — $s = c \cdot \ln(1 + r)$ on the raw image to expand dark regions
7. **Gamma Transform** — $s = c \cdot r^{\gamma}$, $\gamma = 0.5$, to brighten midtones
8. **Comparison Dashboard** — all 7 stages side-by-side

## Output Files (`output/`)

| File | Stage |
|---|---|
| `01_raw_xray.png` | Raw grayscale image |
| `02_equalized_xray.png` | Histogram-equalized image |
| `03_colormap_jet_heatmap.png` | JET colormap heatmap |
| `04_color_balanced.png` | Color-balanced heatmap |
| `05_dense_tissue_threshold.png` | Binary dense-tissue mask |
| `06_logarithmic_transform.png` | Log-transformed image |
| `07_gamma_transform.png` | Gamma-corrected image |
| `08_full_comparison_dashboard.png` | Full pipeline comparison |

## How to Run

1. Open `xray_enhancement.ipynb`.
2. Run all cells top to bottom.
3. Outputs are saved to `output/`.