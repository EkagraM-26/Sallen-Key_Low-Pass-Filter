# 10 kHz 4th-Order Sallen-Key Butterworth Low Pass Filter

## Motivation

Designed as an anti-aliasing filter for a 25 kSPS ADC front-end.

The objective was to attenuate frequencies above the Nyquist limit while maintaining a maximally flat passband response and low distortion.

---

## Filter Architecture

Two cascaded 2nd-order Sallen-Key stages:

Input
→ Stage 1 (Q = 0.541)
→ Stage 2 (Q = 1.306)
→ Output

---

## Design Specifications

| Parameter | Value |
|------------|---------|
| Filter Type | Butterworth |
| Order | 4 |
| Cutoff Frequency | 10 kHz |
| Supply Voltage | ±12 V |
| Op Amp | OPA2134 |
| ADC Sampling Rate | 25 kSPS |

---

## Component Values

### Stage 1

| Component | Value |
|------------|---------|
| R1A | 17.4 kΩ |
| R2A | 41.2 kΩ |
| C1A | 1 nF |
| C2A | 820 pF |

### Stage 2

| Component | Value |
|------------|---------|
| R1B | 17.4 kΩ |
| R2B | 41.2 kΩ |
| C1B | 1 nF |
| C2B | 150 pF |

--- 
## Design Equations

For each Sallen-Key section:

\[
f_0 =
\frac{1}
{2\pi\sqrt{R_1*R_2*C_1*C_2}}
\]

The Butterworth response is achieved by cascading two second-order
sections whose pole locations correspond to:

| Stage | Q |
|---------|---------|
| 1 | 0.5412 |
| 2 | 1.3066 |

Although closed-form component values were calculated initially,
final resistor and capacitor values were refined in LTspice to
obtain the target 10 kHz Butterworth response.

See:

'calculations/design_equations.md'
---

## AC Response

### Magnitude Response

![Magnitude](results/bode_magnitude.png)

### Phase Response

![Phase](results/bode_phase.png)

---

## Step Response

![Step Response](results/step_response.png)

Measured overshoot and settling behavior match Butterworth expectations.

---

## THD Analysis

Input:

- 1 Vrms
- 1 kHz sinewave

Result:

- THD = XX %

(See results/thd_log.txt)

---

## Monte Carlo Analysis

![Monte Carlo](results/monte_carlo_overlay.png)

100-run component tolerance analysis confirms cutoff variation remains within design limits.

---

## Project Files

| Folder | Contents |
|----------|-----------|
| calculations | Design derivations |
| ltspice | Schematics and simulations |
| results | Plots and logs |
| bom | Bill of Materials |
| docs | Full report |

---

## How to Simulate

1. Open LTspice.
2. Load:

   ltspice/sk_lpf_4th_order.asc

3. Run AC analysis:

   Simulate → Run

4. Run transient analysis:

   Open simulations/step_response.asc

5. Run THD analysis:

   Open simulations/thd_analysis.asc

6. Run Monte Carlo:

   Open simulations/monte_carlo.asc

---

## Results Summary

| Metric | Result |
|----------|----------|
| Cutoff Frequency | ~10 kHz |
| Filter Order | 4 |
| Response Type | Butterworth |
| Supply Voltage | ±15 V |
| THD | (from LTspice log) |
| Monte Carlo Runs | 100 |
| Op-Amp | OPA2134 |

---

## Author

Ekagra Maheshwari

B.Tech Electronics & Electrical Engineering

Interested in Analog IC Design, Signal Chain Design, and Embedded Systems.