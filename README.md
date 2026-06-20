# GVH-Dynamique

GVH Dynamic: A Multi-Scale Diagnostic Framework for Critical Regimes in Nonlinear Dynamical Systems

Author: Charlemagne Laurince

Status: Research framework under active development

Version: 0.1.0

GVH Dynamic: A Multi-Scale Diagnostic Framework for Critical Regimes in Nonlinear Dynamical Systems

Overview

GVH-Dynamique is a research framework designed to characterize critical transitions in nonlinear dynamical systems through a set of multi-scale diagnostic indicators.

The framework introduces quantitative measures aimed at detecting changes in dynamical regimes, coherence loss, and the emergence of critical behavior across different classes of systems.

The methodology has been tested on:

* Lorenz system
* Duffing oscillator
* Rössler system
* Control signals (sinusoidal and stochastic)
* Cosmological datasets (Pantheon+)

⸻

Core Metrics

The current implementation includes:

* D : dynamical divergence indicator
* S : coherence indicator
* R_super : super-critical occupation ratio
* B_H : hierarchical dynamic index
* θ_mean : mean opposition angle
* R180 : opposition ratio

These metrics provide complementary information on system organization and regime transitions.

⸻

Repository Structure

GVH-Dynamique/
├── paper/
├── src/
├── cosmology/
├── data/
├── results/
└── notebooks/

⸻

Reproducing Results

Lorenz

Source code:

src/lorenz/

Duffing

Source code:

src/duffing/

Rössler

Source code:

src/rossler/

Cosmology

Source code:

cosmology/

⸻

Installation

pip install -r requirements.txt

⸻

Volume VIII

This repository accompanies:

Volume VIII — GVH Dynamique

Diagnostic Multi-Échelle des Régimes Critiques dans les Systèmes Non Linéaires

⸻

Citation

If you use this repository, please cite:

Laurince, C. (2026).

GVH Dynamic: A Multi-Scale Diagnostic Framework for Critical Regimes in Nonlinear Dynamical Systems.

GitHub repository:
https://github.com/col38470682/GVH-Dynamique

⸻

License

MIT License.
