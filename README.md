# Analog Quadrature Down Converter

![LTspice](https://img.shields.io/badge/LTspice-blue?style=flat-square&logo=ltspice)
![Hardware](https://img.shields.io/badge/Hardware-Validated-brightgreen?style=flat-square)
![Analog Design](https://img.shields.io/badge/Analog-Design-orange?style=flat-square)

This repository contains the complete design, analysis, simulation, and hardware realization of a Quadrature Down Converter (QDC) designed for modern wireless receiver front-ends. Quadrature downconversion is an essential technique used in communication systems (Wi-Fi, Bluetooth, WLAN) to mitigate image interference and allow for zero-IF baseband processing.

## 🚀 Key Specifications
| Parameter | Value |
|-----------|-------|
| **LO Frequency** | 150 kHz |
| **LO Amplitude** | $1 V_{PP}$ |
| **Baseband (IF)** | $\approx 5 \text{ kHz}$ |
| **Low-Pass Filter**| 3 kHz (-3dB cutoff) |
| **Mixer Tech** | TSMC 180nm NMOS |
| **Oscillator** | Dual UA741 Integrator |

---

## 🧩 System Architecture
The QDC system translates a high-frequency RF signal down to an Intermediate Frequency (IF) using two orthogonal local oscillator signals ($0^\circ$ and $90^\circ$). This preserves both the amplitude and phase information of the original complex baseband signal.

The complete system is built from three tightly integrated subsystems:

### 1. Quadrature Oscillator
A robust two-integrator feedback loop employing UA741 operational amplifiers. The amplitude is stabilized to a clean $1 V_{PP}$ without saturation distortion using a soft diode-clipping network (1N4148 pairs). This subsystem produces two sinusoidal signals ($v_{OSCI}$ and $v_{OSCQ}$) with exactly a $90^\circ$ phase difference.

### 2. Dual Switching Mixers
Two discrete NMOS transistors operate in the triode region as voltage-controlled switches. They multiply the incoming RF signal by the orthogonal oscillator signals.

### 3. Baseband Filters & Output Amplifier
The IF outputs from the mixers are filtered by an RC low-pass filter (cutoff $\approx 3.39\text{ kHz}$) to eliminate higher-order harmonics and the sum-frequency components. A non-inverting output amplifier stage was tested to achieve a final signal amplitude of $400 mV_{PP}$.

---

## 🛠️ Repository Structure

```text
├── docs/                   # IEEE Project Report and Diagrams
├── hardware/               # BOM and Hardware Measurement Data
└── simulation/             # LTspice project files
    ├── models/             # Standard models (TSMC 180nm, UA741)
    ├── quadrature_oscillator.asc
    ├── nmos_mixer.asc
    ├── low_pass_filter.asc
    └── qdc_complete.asc
```

---

## 📊 Performance Summary (Simulated vs Measured)
Hardware validation confirmed that the architecture successfully translates the signal and maintains the critical $90^\circ$ relationship at baseband.

| Parameter | Simulated | Measured (Hardware) |
|-----------|-----------|----------------------|
| **Oscillator Frequency** | 145 kHz | 143.8 kHz |
| **Oscillator Amplitude (I/Q)** | $\approx 1 V_{PP}$ | $\approx 0.95 V_{PP}$ |
| **Oscillator Phase Diff** | $90^\circ$ | $88.5^\circ$ |
| **IF Frequency ($f_{IF}$)** | $\|f_{osc} - f_{in}\|$ | $4.97\text{ kHz}$ |
| **IF Final Phase Diff** | $\approx 90^\circ$ | $86.2^\circ$ |

---

## ⚙️ Running the Simulations
1. Clone this repository.
2. Ensure you have **LTspice** installed.
3. Open any `.asc` file in the `simulation/` directory.
4. Run the simulation. The `.inc` directives are already set up to reference the models in `simulation/models/`.

> **Note:** The layout of the `.asc` files might need slight visual rewiring (snapping to grid) depending on your LTspice version and graphics settings, but the netlists and components are fully populated.

---
*Developed as part of the Analog Electronic Circuits course (Spring 2026), IIIT Hyderabad.*
