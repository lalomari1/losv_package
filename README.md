# LOS-V: Variability-based Level of Service Framework 📊🚗

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python](https://img.shields.io/badge/Python-3.7%2B-blue.svg)](https://www.python.org/)

This repository contains the official open-source Python package for the **LOS-V (Variability-based Level of Service)** framework, introduced in the paper:  
> **"Revisiting Level of Service Assessment by Incorporating Speed Variability and Acceleration Noise Using High-Resolution Trajectory Data"** > *Accepted for publication in the Transportation Research Record (TRR).*

---

## 🔍 Overview

Conventional Level of Service (LOS) assessments (e.g., HCM guidelines) rely heavily on macro-level, aggregated measures like average speed. However, aggregate states often mask severe traffic instability and microscopic vehicle oscillations. 

The **LOS-V framework** conceptualizes traffic as a stochastic dynamic system. By processing high-resolution microscopic trajectory data (0.1-second temporal resolution), it integrates:
1. **Speed Coefficient of Variation ($CV_v$)** with a numeric safety constraint at near-zero speeds.
2. **Acceleration Noise ($\sigma_a$)** within a rolling trajectory-smoothing window.

These components are standardized using Z-score normalization into a robust, single composite index ($I_{LOS-V}$) to reveal hidden traffic instabilities, reclassifying traffic states into more operational and dynamic categories (A through F).

---

## 🛠️ Package Architecture

The package is structured modularly for maximum transparency and academic reproducibility:
- `losv/io.py`: Robust column identification and automated trajectory data cleaning.
- `losv/preprocessing.py`: Vehicle-specific moving average filtering and spatiotemporal segmentation.
- `losv/metrics.py`: Mathematical calculation of $CV_v$, acceleration noise, and the spatiotemporal Shockwave Proxy.
- `losv/classification.py`: Quantile-based and fixed-threshold level of service grading.
- `losv/plotting.py`: High-resolution (900 DPI) publication-ready visualization engine.

---

## 🚀 Installation

Clone this repository and install it locally using `pip`:

```bash
git clone [https://github.com/lalomari1/losv_package.git](https://github.com/lalomari1/losv_package.git)
cd losv_package
pip install .

---

## ⚡ Quick Start & Usage
With just a few lines of code, you can execute the entire pipeline, calculate the advanced traffic indicators, and export all 11 scientific figures:
import losv

# 1. Load data and automatically detect columns
data_path = "path_to_your_ngsim_data.csv"
df, detected = losv.load_and_detect_trajectory(data_path)

# 2. Run the processing pipeline
df = losv.smooth_trajectories(df, detected, smooth_window=5)
df = losv.apply_spatiotemporal_segmentation(df, detected, time_window_sec=10, segment_length_ft=500)

# 3. Compute indicators & validation metrics
metrics = losv.compute_segment_metrics(df, min_mean_speed_fts=5.0)
metrics = losv.compute_shockwave_proxy(metrics)

# 4. Classify traffic states
final_results = losv.apply_los_classifications(metrics, alpha=0.5, beta=0.5)

# 5. Export 900 DPI publication-ready figures
losv.plot_all_results(final_results, output_figures_dir="./results/figures", dpi=900)

print("Pipeline completed. Check your results folder!")

---

## 📄 Citation
If you use this framework or package in your transportation research, please cite our TRR paper:

@article{losv2026,
  title={Revisiting Level of Service Assessment by Incorporating Speed Variability and Acceleration Noise Using High-Resolution Trajectory Data},
  author={AlOmari, Laith D.},
  journal={Transportation Research Record},
  year={2026},
  publisher={SAGE Publications}
}
