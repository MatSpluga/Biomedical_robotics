# Assignment 1 – EMG-Based Cursor Control and Robot Arm Reaching

## Overview

This assignment explores the use of a **Myoelectric Computer Interface (MCI)** to control a screen cursor through muscle activity. Surface EMG signals recorded from four muscles are processed to estimate their activation levels. These activations are then mapped to cursor velocity, allowing the cursor trajectory to be reconstructed and compared with the trajectory recorded by the MCI system.

The assignment also includes a reaching-performance analysis and a bonus task in which the reconstructed cursor trajectory drives a simulated planar two-link robot arm.

## Main Topics

- EMG signal preprocessing and activation-envelope extraction.
- Comparison between reconstructed and MCI-computed muscle envelopes.
- Muscle-to-cursor velocity mapping.
- Cursor trajectory reconstruction and error analysis.
- Reaching time and overshoot analysis.
- Resolved-rate control of a planar two-link robot arm.

## Repository Structure

| File / Folder | Description |
|---|---|
| `Assignment1.m` | MATLAB initialization script. |
| `Assignment_1_code/assignment_1_reaching_analysis.m` | Main MATLAB analysis pipeline for Parts 1–5. |
| `Assignment_1_code/Group_6.mat` | Prepared dataset containing EMG, cursor, target, and calibration information. |
| `Assignment_1_code/ID_6_Session_1/` | Original session acquisition data used to prepare the group dataset. |
| `Assignment_1_code/assignment_1.pptx` | Assignment presentation/material. |
| `Report_assignment_1/` | Written report, figures, and LaTeX source files. |

## Analysis Pipeline

### Part 1 – EMG Preprocessing and Envelope Extraction

The raw EMG signals are converted from ADC counts to microvolts and processed using a conventional pipeline:

1. Remove the DC component.
2. Apply a fourth-order Butterworth band-pass filter (30–450 Hz).
3. Rectify the filtered signals.
4. Apply a fourth-order Butterworth low-pass filter at 5 Hz.
5. Normalize each envelope using the corresponding muscle calibration maximum.

The reconstructed envelopes are compared with those computed by the MCI system. Correlation coefficients and cross-correlation-based time delays are evaluated for each muscle. The signals are then downsampled to 100 Hz after envelope extraction.

### Part 2 – MCI Mapping and Cursor Velocity

The four muscle activation envelopes are mapped to the horizontal and vertical cursor velocities using the MCI mapping matrix and its gain. A 5% dead zone is applied to suppress small residual activations.

### Part 3 – Cursor Trajectory Reconstruction

Cursor positions are reconstructed by integrating the estimated velocities over time. The reconstructed trajectory is compared with the logged cursor position, and the mean position error is calculated. An animation can display the logged cursor, reconstructed cursor, and current target.

### Part 4 – Reaching Performance

The analysis considers successfully reached targets and, for the center-out task, excludes central targets to focus on outward reaches. Reach times and overshoot counts are extracted and plotted.

### Part 5 – Bonus: Two-Link Robot Arm

The cursor trajectory is mapped into the workspace of a planar two-link robot arm. The initial joint configuration is obtained through inverse kinematics. The arm then follows the reference trajectory using **resolved-rate control**, based on the manipulator Jacobian and a proportional position-error correction term.

The code evaluates Cartesian tracking errors and monitors the Jacobian determinant to identify proximity to kinematic singularities. It also plots and animates the robot arm motion.

## Requirements

- MATLAB
- Signal Processing Toolbox (`butter`, `filtfilt`, `xcorr`, and related signal-processing functions)
- The provided `.mat` dataset and session data

The main analysis script also calls `make_group_mat` to prepare `Group_6.mat` from the session acquisition files. If this helper function is not available in your MATLAB path, use the already provided `Group_6.mat` and disable or comment out the `make_group_mat(...)` call before running the analysis.

## How to Run

1. Extract the repository while preserving the folder structure.
2. Open MATLAB and set the current folder to `Assignment_1_code`.
3. Ensure that `Group_6.mat` is available in the current folder.
4. Open and run:

   ```matlab
   assignment_1_reaching_analysis
   ```

The script is configured to analyze the `centerout` task by default. The `task`, `animateCursor`, `resetAtEachTarget`, and `animateArm` settings can be changed in the settings section at the beginning of the script.

## Report

The `Report_assignment_1` folder contains the written report (`main.pdf`), its LaTeX source files, and figures generated for the analysis. Consult the report for the detailed methodology, plots, and discussion of the experimental results.
