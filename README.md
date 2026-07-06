# NASA Turbofan Jet Engine Degradation Data Pipeline (KNIME)

This repository contains an automated low-code data engineering pipeline built using **KNIME Analytics Platform** to process, clean, and analyze high-frequency time-series telemetry from the **NASA C-MAPSS (Turbofan Engine Degradation Simulation)** dataset.

## Workflow Architecture
The pipeline automates the ingestion of raw text telemetry, applies signal processing filters, resolves boundary conditions, and applies thermodynamic performance indices to map asset degradation trends.

### Key Engineering Steps
1. **Telemetry Ingestion:** Ingested multivariate space-separated flight-fleet run-to-failure records.
2. **Signal Denoising:** Utilized a 10-cycle backward Simple Moving Average (SMA) filter to isolate authentic thermal patterns from instrument noise.
3. **Feature Engineering:** Calculated the dimensionless **Turbine Temperature Ratio (TTR)** (T50 / T30) to evaluate the progressive health drop of the turbine assembly.

## Results
By isolating a single asset (Engine ID #1), the workflow successfully maps a continuous wear curve revealing a steep increase in operational thermal stress as the engine approaches structural failure.

## How to Run
1. Download and install KNIME Analytics Platform.
2. Download the `.knwf` workflow file from this repository and import it into your workspace.
3. Supply the raw NASA `train_FD001.txt` dataset to the CSV Reader node.
