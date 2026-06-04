# 4th-Order Butterworth Sallen-Key Low-Pass Filter

## Design Objective

Design a 4th-order Butterworth low-pass filter with:

- Cutoff frequency: 10 kHz
- Passband ripple: 0 dB
- Anti-aliasing front-end for a 25 kSPS ADC
- Supply voltage: ±15 V
- Op-amp: OPA2134

---

## Butterworth Pole Locations

A 4th-order Butterworth response can be realized by cascading two
2nd-order sections with:

| Stage | Q |
|---------|---------|
| Stage 1 | 0.5412 |
| Stage 2 | 1.3066 |

---

## General Sallen-Key Transfer Function

For a unity-gain Sallen-Key low-pass filter:

\[
\omega_0 =
\frac{1}
{\sqrt{R_1R_2C_1C_2}}
\]

\[
f_c=
\frac{1}
{2\pi\sqrt{R_1R_2C_1C_2}}
\]

The quality factor is

\[
Q=
\frac{\sqrt{R_1R_2C_1C_2}}
{C_1(R_1+R_2)}
\]

for the chosen topology.

---

## Final Optimized Component Values

### Stage 1

| Component | Value |
|------------|---------|
| R1A | 17.4 kΩ |
| R2A | 41.2 kΩ |
| C1A | 1 nF |
| C2A | 820 pF |

---

### Stage 2

| Component | Value |
|------------|---------|
| R1B | 17.4 kΩ |
| R2B | 41.2 kΩ |
| C1B | 1 nF |
| C2B | 150 pF |

---

## Stage 1 Natural Frequency

\[
f_{01}
=
\frac{1}
{2\pi
\sqrt{
(17.4k)
(41.2k)
(1n)
(820p)
}}
\]

\[
f_{01}
\approx 6.57\ kHz
\]

---

## Stage 2 Natural Frequency

\[
f_{02}
=
\frac{1}
{2\pi
\sqrt{
(17.4k)
(41.2k)
(1n)
(150p)
}}
\]

\[
f_{02}
\approx 15.37\ kHz
\]

---

## Implementation Notes

Theoretical equal-value resistor solutions were evaluated initially.
Final component values were refined through LTspice simulation to obtain
the desired overall 4th-order Butterworth response and cutoff frequency.

The final design uses:

- OPA2134 dual audio op-amp
- ±15 V supply rails
- C0G/NP0 capacitors
- 1% metal-film resistors

---

## Verification

The final filter was verified using:

1. AC sweep (Bode magnitude and phase)
2. Step response
3. Fourier / THD analysis
4. Monte-Carlo tolerance analysis

All simulation files are available in the LTspice folder.