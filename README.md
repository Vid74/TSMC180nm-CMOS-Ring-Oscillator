# 5-Stage CMOS Ring Oscillator using TSMC 180 nm | LTspice Characterization

![LTspice](https://img.shields.io/badge/Tool-LTspice-red)
![Technology](https://img.shields.io/badge/Technology-TSMC%20180nm-blue)
![Design](https://img.shields.io/badge/Design-CMOS%20Ring%20Oscillator-green)
![Simulation](https://img.shields.io/badge/Simulation-BSIM3%20Level49-orange)
![Status](https://img.shields.io/badge/Status-Completed-success)

---

## Project Overview

This project presents the complete **design, simulation, characterization, and optimization** of a **5-stage CMOS Ring Oscillator** implemented using **TSMC 180 nm BSIM3 Level-49 transistor models** in **LTspice**.

The oscillator consists of five CMOS inverter stages connected in a closed feedback loop to generate sustained oscillations without requiring any external clock source. The project focuses not only on circuit implementation but also on comprehensive performance characterization under different operating conditions, similar to the validation process followed during ASIC IP development.

Multiple analyses including frequency measurement, propagation delay, startup behavior, power consumption, temperature dependence, supply voltage variation, load capacitance analysis, and transistor sizing optimization were performed to evaluate oscillator performance and validate theoretical predictions.

---

# Project Objectives

- Design a 5-stage CMOS Ring Oscillator
- Optimize CMOS inverter sizing
- Verify oscillator startup
- Measure oscillation frequency
- Calculate propagation delay
- Compare theoretical and simulated results
- Analyze power consumption
- Characterize temperature dependence
- Analyze supply voltage sensitivity
- Study load capacitance effects
- Optimize transistor sizing
- Calculate Energy per Cycle
- Calculate Power Delay Product (PDP)

---

# Technology Specifications

| Parameter | Value |
|-----------|-------|
| Technology | TSMC 180 nm |
| Transistor Model | BSIM3 Level-49 |
| Simulator | LTspice XVII |
| Supply Voltage | 1.8 V |
| Number of Stages | 5 |
| NMOS Size | 1 µm / 180 nm |
| PMOS Size | 2 µm / 180 nm |
| Oscillator Type | CMOS Ring Oscillator |

---

# Ring Oscillator Theory

A Ring Oscillator is formed by connecting an **odd number of CMOS inverters** in a feedback loop.

Each inverter contributes:

- 180° phase inversion
- Propagation delay

The total delay around the loop causes continuous switching, resulting in sustained oscillations.

The oscillation frequency is given by

\[
f=\frac{1}{2Nt_{pd}}
\]

where

- **N** = Number of inverter stages
- **tpd** = Average propagation delay of one inverter

---

# Design Flow

```

CMOS Inverter Design
↓
Inverter Verification
↓
5-Stage Ring Oscillator
↓
Startup Verification
↓
Frequency Measurement
↓
Delay Measurement
↓
Temperature Analysis
↓
Supply Voltage Analysis
↓
Power Analysis
↓
Load Capacitance Analysis
↓
Transistor Sizing Optimization
↓
Performance Validation

```

---

# Project Directory Structure

```

CMOS-5Stage-Ring-Oscillator/

│
├── Design/
│   ├── RingOscillator.asc
│   ├── CMOS_Inverter.asc
│   ├── TSMC180nm.lib
│
├── Results/
│   ├── Startup Waveform.png
│   ├── Frequency Measurement.png
│   ├── Delay Measurement.png
│   ├── Frequency_vs_Temperature.png
│   ├── Delay_vs_Temperature.png
│   ├── Frequency_vs_VDD.png
│   ├── Power_vs_Temperature.png
│   ├── Load_Capacitance.png
│
├── Report/
│   └── Ring Oscillator Report.pdf
│
└── README.md

```

---

# Circuit Design

The oscillator consists of

- Five CMOS Inverters
- TSMC 180 nm BSIM3 MOSFET models
- Positive feedback connection
- Supply Voltage = 1.8 V

### CMOS Inverter Sizing

| Device | Width | Length |
|---------|-------|---------|
| NMOS | 1 µm | 180 nm |
| PMOS | 2 µm | 180 nm |

The PMOS width is chosen approximately twice that of the NMOS to compensate for the lower hole mobility and obtain nearly equal rise and fall delays.

---

# Simulation Setup

Transient Simulation

```

.tran 0 100n startup

```

Supply Voltage

```

VDD = 1.8 V

```

Measurements

```

.meas
.param
.step

```

Technology Library

```

TSMC180nm.lib

```

---

# Characterization Performed

## 1. Oscillation Verification

Verified successful oscillator startup using transient simulation.

### Observation

- Stable oscillation achieved
- Full voltage swing observed

---

## 2. Frequency Measurement

Measured oscillation frequency using LTspice measurement commands.

### Result

- Oscillation Frequency ≈ **1.64 GHz**

---

## 3. Propagation Delay

Measured average inverter delay.

### Result

- Propagation Delay ≈ **57 ps**

---

## 4. Frequency Validation

Theoretical frequency

\[
f=\frac{1}{2Nt_{pd}}
\]

Simulation results closely matched theoretical calculations with approximately **6% deviation**, primarily due to transistor nonlinearity and parasitic capacitances.

---

## 5. Frequency vs Temperature

Temperature sweep performed

```

0°C
25°C
50°C
75°C
100°C

```

### Observation

Frequency decreases as temperature increases.

### Reason

Higher temperature reduces carrier mobility, increasing propagation delay.

---

## 6. Delay vs Temperature

Measured inverter delay across multiple temperatures.

### Observation

Propagation delay increases with temperature.

---

## 7. Average Power Consumption

Average supply current measured using

```

.meas tran Iavg AVG I(VDD)

```

Power calculated as

\[
P=V_{DD}\times I_{avg}
\]

### Observation

Power decreases with increasing temperature due to lower switching frequency.

---

## 8. Frequency vs Supply Voltage

Supply voltage sweep

```

1.2 V
1.4 V
1.6 V
1.8 V
2.0 V

```

### Observation

Higher supply voltage increases oscillation frequency.

---

## 9. Load Capacitance Analysis

Load capacitance sweep

```

10 fF
20 fF
50 fF
100 fF
200 fF

```

### Observation

Increasing load capacitance reduces oscillation frequency due to higher RC delay.

---

## 10. Transistor Sizing Optimization

Different NMOS and PMOS widths were analyzed.

### Observation

Increasing transistor width

- increases drive strength
- reduces delay
- increases frequency
- increases power consumption

---

## 11. Energy per Cycle

Calculated using

\[
Energy=\frac{Power}{Frequency}
\]

This metric represents the energy consumed during one oscillation cycle.

---

## 12. Power Delay Product

Calculated as

\[
PDP=P\times t_{pd}
\]

PDP is a standard metric used to evaluate the energy efficiency of CMOS circuits.

---

# Performance Summary

| Parameter | Result |
|-----------|--------|
| Technology | TSMC 180 nm |
| Supply Voltage | 1.8 V |
| Oscillator Stages | 5 |
| Oscillation Frequency | ~1.64 GHz |
| Propagation Delay | ~57 ps |
| Startup | Successful |
| Output Swing | Rail-to-Rail |
| Temperature Sweep | Completed |
| Voltage Sweep | Completed |
| Power Analysis | Completed |
| Load Sweep | Completed |
| Sizing Optimization | Completed |

---

# Key Learning Outcomes

This project demonstrates

- CMOS inverter design
- Ring oscillator operation
- BSIM3 MOSFET modeling
- LTspice simulation
- Transient analysis
- Frequency measurement
- Delay analysis
- Power characterization
- PVT sensitivity
- Design optimization
- Performance trade-off analysis

---

# Future Improvements

The following enhancements can further improve the design:

- Output Buffer Design
- Current-Starved VCO
- PLL Integration
- Phase Noise Analysis
- Jitter Analysis
- Monte Carlo Analysis
- Process Corner Analysis (TT/SS/FF)
- Layout Design
- DRC/LVS Verification
- Post-Layout Simulation

---

# Applications

- PLLs
- Clock Generators
- On-Chip Clock Distribution
- Random Number Generators
- Built-In Self-Test (BIST)
- Process Monitoring
- Frequency Sensors
- Digital Timing Circuits

---

# References

1. TSMC 180 nm CMOS Technology Documentation
2. LTspice XVII User Guide
3. Razavi, B., *Design of Analog CMOS Integrated Circuits*
4. Weste & Harris, *CMOS VLSI Design*
5. Jan M. Rabaey, *Digital Integrated Circuits*

---

# Author

**Sri Vid**

Electronics and Communication Engineering

VLSI | Digital Design | Analog Design | LTspice | Verilog | FPGA

---
⭐ If you found this project useful, consider starring the repository.
