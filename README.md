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
