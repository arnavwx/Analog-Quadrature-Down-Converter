# Quadrature Oscillators

## The Barkhausen Criterion
For an electronic circuit to exhibit sustained oscillations, it must form a closed feedback loop that satisfies the Barkhausen criterion:
1. **Loop Gain Magnitude**: $| \beta A | \ge 1$ (The gain around the loop must be at least unity).
2. **Loop Phase Shift**: $\angle \beta A = 2\pi n$ (The phase shift around the loop must be a multiple of $360^\circ$).

## Quadrature Generation
In an analog Quadrature Down Converter (QDC), the local oscillator must produce two identical sinusoids that are exactly $90^\circ$ out of phase ($I$ and $Q$). There are three common ways to achieve this:

1. **RC Polyphase Filters**: Taking a differential LO signal and passing it through a complex network of resistors and capacitors to shift the phases. (Disadvantage: Highly sensitive to component mismatch and lossy).
2. **Divide-by-Two Circuits**: Running a VCO at twice the desired frequency ($2\omega$) and passing it through a digital flip-flop divider. (Disadvantage: Burns significant power and requires $2\times$ frequency capability).
3. **Coupled Oscillators (Quadrature VCOs)**: Cross-coupling two identical LC or RC oscillators such that they force each other to operate in quadrature.

## The Sine-Wave Quadrature Oscillator
For lower frequency analog testing, a standard approach is to use Op-Amp based integrators. 
An ideal integrator has a transfer function of $H(s) = \frac{-1}{RCs}$, which introduces an exact $90^\circ$ phase shift at all frequencies.

By cascading two integrators in a loop:
- Integrator 1: $90^\circ$ phase shift.
- Integrator 2: $90^\circ$ phase shift.
- Inversion in the loop: $180^\circ$ phase shift.
- Total Phase Shift: $360^\circ$ (satisfying Barkhausen).

If we extract the output of the first integrator, it will be exactly $90^\circ$ offset from the output of the second integrator, yielding perfectly matched Sine and Cosine waves. In practical design, amplitude stabilization circuitry (like back-to-back diodes) is added to prevent the amplitude from clipping against the op-amp supply rails.
