# Space-debris-lidarsim
A 3D Python simulation mapping space debris trajectories and classifying collision hazards using LiDAR telemetry data.
# Autonomous 3D Space Debris Detection & Hazard Classification Simulator

An engineering-grade Python simulation that models a stationary orbital LiDAR tracking station monitoring and classifying the kinematic trajectories of space debris in a 3D coordinate system. 

This project demonstrates the practical application of 3D kinematics, algorithmic threat classification, stochastically generated sensor noise, and dynamic 3D data visualization.

---

## 🚀 System Features
- **3D Trajectory Kinematics:** Simulates true physical vector positions (X, Y, Z) using decoupled multi-axis velocities over discrete time increments (Δ t).
- **Stochastic Noise Generation:** Models real-world hardware imperfections by injecting a uniform random distribution of signal noise (± 0.3m) into distance calculations.
- **Autonomous Threat Assessment:** Implements a real-time cascading threshold logic network to automatically classify approaching objects into distinct danger matrices (`SAFE`, `WARNING`, `CRITICAL`).
- **Interactive Spatial Plotting:** Generates dynamic 3D data matrices using Matplotlib to map the tracked telemetry relative to the sensor origin.

---

## 📊 Mathematical & Architectural Overview

The tracking station is positioned symmetrically at the coordinate origin (0, 0, 0). 

### 1. Kinematic Position Tracking
For each discrete time step (dt), the absolute position updates along all three spatial vectors independently:
\[X_{t} = X_{t-1} + (V_x \cdot dt)\]
\[Y_{t} = Y_{t-1} + (V_y \cdot dt)\]
\[Z_{t} = Z_{t-1} + (V_z \cdot dt)\]

### 2. 3D Ranging Formula
The true geometric distance (\(D_{\text{true}}\)) between the tracking origin and the moving target is calculated using the 3D expansion of the Pythagorean Theorem:
\[D_{\text{true}} = \sqrt{X^2 + Y^2 + Z^2}\]

### 3. Environmental Error Factor
To mirror raw sensor telemetry, an unpredictable noise coefficient (ε) is applied to yield the final measured range (\(D_{\text{measured}}\)):
\[D_{\text{measured}} = D_{\text{true}} + \epsilon \quad \text{where} \quad \epsilon \sim \mathcal{U}(-0.3, 0.3)\]

---

## 🛠️ Project Structure & Execution

### Prerequisites
The core simulation runs natively on standard Python configurations. The interactive visual tracking dashboard requires `matplotlib` and `ipympl` (for cloud-based widget architectures like Google Colab).

```bash
pip install matplotlib ipympl
```

### Script Implementation
The full executable file handles everything inside a unified execution loop:
1. **Initializes the Spatial Matrix** with defined structural velocities.
2. **Computes Telemetry Loops** extracting range vectors at designated intervals.
3. **Applies Detection Filters** to alert systems of proximity anomalies.
4. **Triggers Matplotlib Rendering Engines** to build the 3D telemetry display.

---

## 📈 System Output Display
When compiled, the script tracks object vectors inside the command line environment before launching an interactive 3D spatial mapping window:

```text
--- STARTING ACTIVE DEBRIS DETECTION SIMULATION ---
Time: 1s | True Pos: (1.50, 10.50, 6.00)m
       | LiDAR Measured Distance: 12.14m (Error: 0.05m)
       | Threat Assessment: 🚨 CRITICAL: Immediate Collision Hazard!
------------------------------------------------------------
Time: 2s | True Pos: (3.00, 11.00, 7.00)m
       | LiDAR Measured Distance: 13.56m (Error: -0.19m)
       | Threat Assessment: 🚨 CRITICAL: Immediate Collision Hazard!
------------------------------------------------------------
Time: 3s | True Pos: (4.50, 11.50, 8.00)m
       | LiDAR Measured Distance: 14.81m (Error: 0.12m)
       | Threat Assessment: ⚠️ WARNING: Object entering proximity vector.
...
```

---

## Application Context
This project was conceptualized and coded independently as a project to investigate the effectiveness of navigation in space. It serves as tangible evidence of:
- Mastery of array-based data tracking using sequential iterations.
- Practical translation of multi-variable physics principles into reliable software logic.
- Understanding of data representation and the extraction of visual insights from numeric telemetry.
