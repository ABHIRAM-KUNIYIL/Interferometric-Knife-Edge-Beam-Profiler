# Interferometric Knife-Edge Beam Profiler

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![SciPy](https://img.shields.io/badge/SciPy-Signal_Processing-lightgrey)
![Optics](https://img.shields.io/badge/Physics-Optics-success)

A robust Python data analysis pipeline for extracting sub-micrometre laser beam waists ($w_0$) using a continuous voice-coil knife-edge scanner and in-situ Michelson interferometry. 

This repository contains the signal processing and statistical fitting code used to characterize tightly focused beams, particularly useful for optical trapping and atomic physics applications where beam profile accuracy directly dictates trap depths and heating rates.

 Overview

Conventional high-resolution knife-edge measurements rely on expensive piezo actuators with limited stroke ranges. This project demonstrates a low-cost, high-stroke alternative using an electromagnetic actuator (a repurposed audio speaker). Because speaker suspension is non-linear, a co-mounted Michelson interferometer ($\lambda = 516$ nm) is used to generate an absolute, strictly calibrated position axis.

This script processes the raw oscilloscope data, tackling heavy 8-bit analog-to-digital (ADC) quantization noise that causes standard phase-extraction (like Hilbert transforms) to fail.

Key Features

* **Zero-Crossing Fringe Counting:** A custom algorithm that AC-couples, smooths, and extracts exactly $\lambda/4$ (129 nm) positional steps based purely on the sign transitions of the interferometer signal, rendering the calibration immune to ADC amplitude quantization.
* **Model-Free Geometric Extraction:** Automatically calculates $10\%-90\%$ and $1/e^2$ transition widths to establish strict, model-free physical boundaries for the beam waist.
* **Statistical Least-Squares Fitting:** Fits the normalized transmission data to a theoretical complementary error function (`erfc`) to determine the primary beam waist with sub-micrometre covariance uncertainty.
* **Beam Profile Reconstruction:** Calculates the numerical derivative of the S-curve, suppressing edge artifacts, to visually reconstruct the physical Gaussian ($TEM_{00}$) intensity profile.

Requirements

The script relies on standard scientific Python libraries.

```bash
pip install numpy scipy matplotlib
