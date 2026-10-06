# RF Mixers and the NMOS Mixer Topology

## Introduction to RF Mixers
A mixer is a non-linear or time-varying electrical circuit that creates new frequencies from two signals applied to it. In its most common application in RF systems, two signals at frequencies $f_1$ (RF) and $f_2$ (LO) are applied to a mixer, and it produces new signals at the sum ($f_1 + f_2$) and difference ($f_1 - f_2$) frequencies.

In the case of a down-converter, we are interested in the difference frequency (IF). 

Mathematically, an ideal mixer is simply an analog multiplier:
$$ v_{out}(t) = \left( A \cos(\omega_{RF} t) \right) \cdot \left( B \cos(\omega_{LO} t) \right) = \frac{AB}{2} \left[ \cos((\omega_{RF} - \omega_{LO})t) + \cos((\omega_{RF} + \omega_{LO})t) \right] $$

The sum frequency is then filtered out using a Low Pass Filter (LPF), leaving only the baseband signal.

## Passive vs. Active Mixers
- **Passive Mixers**: Typically use diodes or passive FET switches. They require zero DC power, exhibit excellent linearity (high IIP3), and very low 1/f noise. However, they suffer from Conversion Loss (the output signal is smaller than the input) and require a massive LO drive signal to switch the diodes/FETs quickly.
- **Active Mixers**: Based on transistors in saturation (e.g., the Gilbert Cell). They provide Conversion Gain, lowering the noise requirements of subsequent stages. They consume DC power and typically have worse linearity and 1/f noise compared to passive mixers.

## The Single NMOS Mixer
For this project, a simplified active/passive NMOS mixer approach is utilized.
A single NMOS transistor is biased such that it operates in the triode (linear) region when acting as a passive switch, or in saturation when acting as an active mixer. 

In a basic NMOS switching mixer:
- The **LO signal** is applied to the **Gate**. This large signal acts as a switch, rapidly turning the transistor ON and OFF.
- The **RF signal** is applied to the **Drain** (or Source).
- The **IF signal** is extracted from the **Source** (or Drain).

By driving the gate with a strong local oscillator signal, the channel resistance $R_{DS}$ is modulated at $\omega_{LO}$. The RF signal passing through this time-varying resistance results in frequency translation.

### Important Mixer Metrics
1. **Conversion Gain / Loss**: The ratio of the IF output power to the RF input power.
2. **Noise Figure (NF)**: The degradation of the Signal-to-Noise Ratio (SNR) caused by the mixer itself. 1/f noise is highly critical in Direct Conversion.
3. **Port Isolation**: 
   - **LO-RF Isolation**: Prevents the strong LO signal from leaking back out the antenna and radiating.
   - **LO-IF Isolation**: Prevents the LO from swamping the baseband amplifiers.
4. **Linearity (1dB Compression and IP3)**: Defines the maximum signal the mixer can handle before intermodulation distortion ruins the signal.
