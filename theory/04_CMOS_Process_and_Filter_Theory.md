# CMOS Process and Filter Theory

## TSMC 180nm CMOS Technology
The Taiwan Semiconductor Manufacturing Company (TSMC) 180nm (0.18 $\mu$m) process is a deeply studied and highly reliable semiconductor fabrication node. While modern consumer electronics operate on 3nm or 5nm nodes, the 180nm node is heavily utilized in analog and mixed-signal design (like RF transceivers) due to its excellent analog matching, high voltage tolerance, and cost-effectiveness.

### Key Characteristics in Analog Design
1. **Threshold Voltage ($V_t$)**: Typically around 0.4V to 0.5V. This allows analog designers enough voltage headroom when operating from 1.8V supplies.
2. **Channel Length Modulation ($\lambda$)**: In shorter channels, the drain current $I_D$ is no longer perfectly independent of $V_{DS}$ in saturation. This creates a finite output resistance $r_o = \frac{1}{\lambda I_D}$, which limits the maximum intrinsic gain ($g_m r_o$) of a single amplifier stage.
3. **Transition Frequency ($f_T$)**: The frequency at which the short-circuit current gain drops to unity. For 180nm NMOS, $f_T$ is roughly 40-50 GHz, making it more than capable of handling RF signals in the low GHz range.

## Low Pass Filter (LPF) Theory
Once the RF signal is mixed down, the resulting signal contains the baseband signal (near DC) and a high-frequency image at $2\omega_{LO}$. A Low Pass Filter is utilized to strip away the high-frequency components.

### Active vs. Passive Filters
- **Passive Filters**: Constructed using Resistors, Capacitors, and Inductors. They are unconditionally stable but cause signal attenuation.
- **Active Filters**: Utilize Op-Amps in feedback with RC networks. They can provide voltage gain while filtering and do not require bulky inductors.

### Butterworth Response
The Butterworth filter is designed to have a frequency response that is as flat as possible in the passband (Maximally Flat Magnitude). Unlike Chebyshev filters, it has no ripple in the passband, ensuring the downconverted baseband signal is not distorted in amplitude.

The trade-off is that the Butterworth filter has a slower roll-off in the transition band. An $N$-th order Butterworth filter rolls off at $-20N$ dB/decade. 

### The UA741 Op-Amp
The UA741 is a classic, general-purpose operational amplifier. In the context of RF and IF filtering, the most critical parameter of an op-amp is its **Gain-Bandwidth Product (GBWP)**.
The 741 has a GBWP of roughly 1 MHz to 1.5 MHz. Because active filters require the op-amp to have excess open-loop gain to enforce the feedback equations properly, the UA741 is strictly limited to lower IF frequencies (audio or low kHz ranges). For true RF IF stages, high-speed op-amps or passive LC filters are strictly required.
