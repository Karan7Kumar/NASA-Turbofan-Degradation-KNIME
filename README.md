# NASA C-MAPSS Turbofan Engine Health Monitoring Pipeline

An enterprise-grade predictive maintenance and health monitoring (HUMS) data pipeline engineered in KNIME to process high-frequency time-series telemetry from the NASA C-MAPSS dataset. 

The core system architecture maps transient thermodynamic metrics across compressor and turbine assemblies to isolate structural degradation signatures from background instrumentation noise.

---

## 🏗️ Project Evolution & Architecture

This repository highlights a multi-phased engineering scaling approach:

### 📍 Phase 1: Single-Engine Baseline
* **Scope:** Isolated high-pressure compressor (HPC) wear profiles under a stable, single sea-level operating condition (`FD001`).
* **Implementation:** Designed foundational automated ingestion, handled primary data arrays, and engineered the core dimensionless tracking index: the **Turbine Temperature Ratio** ($T_{50} / T_{30}$).

### 📍 Phase 2: Parallel Multi-Fleet Scaling (Current Iteration)
* **Scope:** Refactored the core pipeline framework to scale across multiple sub-fleets simultaneously, balancing varied operating regimes (fluctuating altitudes, Mach numbers, and throttle conditions) and dual-fault configurations (`FD001` through `FD004`).
* **Advanced Pipeline Nodes Added:**
  * **Parallel Ingestion & Metadata Tagging:** Built 4 simultaneous ingestion branches. Integrated a **Constant Value Column Appender** to inject dataset identifiers before row concatenation, preserving complete lineage tracking.
  * **Backward Gaussian Moving Average:** Upgraded standard windowing to a Gaussian weighted-sum filter (Window Size = 10) to optimize the noise reduction vs. phase delay (lag) tradeoff.
  * **Multi-Criterion Regex Filtering:** Structured a centralized boolean isolation node `(Engine_ID == 1 AND Dataset_ID == FD001|FD003)` to cleanly extract contrasting lifecycles.

---

## 🧪 Thermodynamic Core Principles

As gas turbine components degrade due to blade erosion or tip clearance growth, aerodynamic efficiencies plummet. To maintain required thrust baselines, fuel flow increments alter engine internal station conditions. 

By calculating the **Turbine Temperature Ratio (TTR)**:

$$\text{TTR} = \frac{T_{50}}{T_{30}}$$

where:
* $T_{30}$ = Total Temperature at High-Pressure Compressor Outlet
* $T_{50}$ = Total Temperature at Low-Pressure Turbine Outlet

The pipeline maps the precise point where thermal signatures diverge from their nominal status, giving automated maintenance, repair, and overhaul (MRO) networks a visual predictive warning long before structural breakdown occurs.

---

## 💻 How to Run the Workflows
1. Download and install the latest desktop edition of **KNIME Analytics Platform**.
2. Clone or download this repository.
3. Import the desired `.knwf` file from the workspace directory.
4. Set your local file path pointers inside the **CSV Reader** blocks to match your copy of the NASA C-MAPSS text files and click **Execute All**.
