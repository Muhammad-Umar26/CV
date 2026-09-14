# Task 3: Real-Time Echocardiogram Video Analysis

Processes each frame of an echocardiogram clip through grayscale conversion, histogram equalization, JET colormapping, color balance, and log/gamma transforms — including a real-time `while`-loop pass over the full video — to improve chamber visibility and suppress speckle noise.

## Dataset

- **Video:** `0X100F044876B98F90.mp4` — cardiac ultrasound clip, loaded from `data/0X100F044876B98F90.mp4`

## Pipeline

1. **Grayscale Conversion** (`cv2.cvtColor`) — convert each frame to a single-channel intensity matrix
2. **Histogram Equalization** (`cv2.equalizeHist`) — restore contrast lost in ultrasound murk
3. **JET Colormap** (`cv2.applyColorMap`) — highlight blood flow intensity vs. tissue density
4. **Color Balance** — per-channel gains ($R{\times}1.15$, $G{\times}0.95$, $B{\times}0.90$)
5. **Logarithmic Transform** — expand dark ventricle/atrium interiors
6. **Gamma Transform** — $\gamma = 1.4$ to suppress bright speckle/backscatter noise
7. **Monitoring Array** — raw vs. enhanced frames sampled across the video and compared side-by-side
8. **Real-Time Processing Loop** (`cv2.VideoCapture` + `while`) — reads every frame continuously, concatenates raw and enhanced side-by-side, and displays them live with `cv2.imshow()` when a display is available; otherwise saves periodic screenshots to `output/` instead

## Output Files (`output/`)

| File | Stage |
|---|---|
| `01_echo_raw_frame.png` | First raw frame from the video |
| `02_echo_enhanced_frame.png` | Same frame after full pipeline |
| `03_echo_side_by_side_pipeline.png` | Raw vs. enhanced comparison |
| `echo_processed_preview.png` | 4-frame monitoring grid (raw + enhanced) |
| `04_live_loop_frame_####.png` | Evidence frames saved during the real-time `while` loop (headless fallback) |

## How to Run

1. Open `realtime_echo.ipynb`.
2. Run all cells top to bottom.
3. Outputs are saved to `output/`.
