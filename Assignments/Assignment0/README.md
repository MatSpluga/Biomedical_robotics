# Assignment 0 – Biological Signal Data Analysis

## Overview

This assignment introduces the analysis of biological signals in the context of **Biomedical Robotics**. The goal is to inspect three provided datasets, visualize their behaviour, identify the likely signal type, and estimate their frequency content.

The datasets correspond to three types of signals:
- **EMG (Electromyography):** electrical activity produced by muscles.
- **Motion data:** movement-related measurements, represented here by a two-dimensional trajectory.
- **EEG (Electroencephalography):** electrical activity of the brain.

## Repository Contents

| File | Description |
|---|---|
| `Assignment0.m` | MATLAB script for loading, plotting, and inspecting the datasets. |
| `Assignment_0.pdf` | Assignment instructions. |
| `data1.mat` | First dataset (sampling frequency: 2000 Hz). |
| `data2.mat` | Second dataset (sampling frequency: 166 Hz). |
| `data3.mat` | Third dataset (sampling frequency: 250 Hz). |

## Implementation

The MATLAB script performs the following steps:

1. **Data loading:** imports the three `.mat` files and extracts the corresponding signals.
2. **Time-domain visualization:** plots each dataset. The second dataset is represented as a two-dimensional trajectory.
3. **Frequency-domain inspection:** computes the Fourier transform using `fftshift` and plots the magnitude spectrum.
4. **Signal interpretation:** uses the shape and characteristics of the plots to associate the datasets with EMG, motion, and EEG signals.

The sampling frequencies are specified in the script:
- `data1`: 2000 Hz
- `data2`: 166 Hz
- `data3`: 250 Hz

## Requirements

- MATLAB
- The three provided `.mat` files in the same folder as `Assignment0.m`

No additional MATLAB toolbox is required for the basic operations used in this script.

## How to Run

1. Open MATLAB.
2. Set the current working directory to the `Assignment0` folder.
3. Run:

   ```matlab
   Assignment0
   ```

The script opens figures showing the datasets in the time domain and their Fourier-transform magnitude spectra.

## Notes

The frequency-domain plots provide a qualitative view of the signals' frequency content. For a physically meaningful frequency axis, the frequency vector should be centred consistently with the use of `fftshift` (for example, by using `(-N/2:N/2-1) * fs/N` for even-length signals).

The signal classifications and frequency estimates should be interpreted together with the time-domain plots and the known sampling frequencies.
