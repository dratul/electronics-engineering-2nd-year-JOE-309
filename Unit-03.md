# Unit 03: Bipolar Junction Transistors and Field-Effect Transistors

**Author:** Dr. Atul Kumar Dwivedi

This guide covers BJT construction and operation, CB/CE/CC configurations, DC bias and stabilization, amplifier action and small-signal analysis, JFET characteristics and CS amplifiers, and depletion- and enhancement-mode MOSFETs.

## Learning objectives

- Explain transistor carrier action and identify operating regions.
- Relate BJT currents and compare CB, CE, and CC configurations.
- Find a transistor's DC operating point (Q-point) for common bias circuits.
- Estimate voltage gain using the midband $r_e$ model.
- Interpret JFET and MOSFET characteristics and calculate simple operating points.

## 1. Bipolar junction transistor (BJT)

A BJT has three doped regions and two PN junctions: emitter, base, and collector. NPN and PNP devices have opposite carrier polarities. The emitter is heavily doped to inject carriers, the thin base controls how many injected carriers reach the collector, and the collector collects carriers and dissipates heat.

### Basic operation and current relations

In the forward-active region, the base-emitter junction is forward biased and the base-collector junction is reverse biased. A small base current controls a larger collector current:

$$
I_E=I_C+I_B,\qquad
\beta=\frac{I_C}{I_B},\qquad
\alpha=\frac{I_C}{I_E}
$$

The current gains are related by:

$$
\beta=\frac{\alpha}{1-\alpha},\qquad
\alpha=\frac{\beta}{\beta+1}
$$

These are approximate device relationships; leakage and temperature affect real transistor currents.

### Operating regions

- **Cutoff:** Both junctions are not forward conducting; collector current is approximately zero.
- **Forward active:** Used for linear amplification.
- **Saturation:** Both junctions are forward biased; the transistor is strongly on and $V_{CE}$ is small but nonzero.
- **Reverse active:** The junction roles are reversed; this is rarely used in ordinary circuits.

For an amplifier, the Q-point must leave room for the signal to swing without clipping into cutoff or saturation.

## 2. BJT configurations

| Configuration | Common terminal | Approximate input/output resistance | Phase relation | Typical feature |
|---|---|---|---|---|
| Common base (CB) | Base | Low input, high output | Non-inverting voltage | Low current gain, useful at higher frequencies |
| Common emitter (CE) | Emitter | Medium input and output | Inverting voltage | High voltage and current gain |
| Common collector (CC) / emitter follower | Collector | High input, low output | Non-inverting | Voltage gain near 1; useful as a buffer |

These are qualitative comparisons; actual resistance and gain depend on the transistor and surrounding circuit.

## 3. DC biasing and the Q-point

Biasing establishes the quiescent (no-signal) values of collector current $I_{CQ}$ and collector-emitter voltage $V_{CEQ}$. A DC load-line equation for a simple collector resistor is:

$$
V_{CE}=V_{CC}-I_C R_C
$$

Select a Q-point within the active region with enough voltage and current headroom for the expected signal.

### Fixed-base bias

For an NPN transistor with base resistor $R_B$ from $V_{CC}$ and emitter grounded:

$$
I_B\approx\frac{V_{CC}-V_{BE}}{R_B},\qquad
I_C\approx\beta I_B,\qquad
V_{CE}\approx V_{CC}-I_C R_C
$$

This circuit is simple, but $I_C$ is sensitive to $\beta$ and temperature.

### Emitter bias

An emitter resistor provides negative feedback: if current rises, the emitter voltage rises, reducing $V_{BE}$ and opposing the change. For a base voltage $V_B$:

$$
V_E\approx V_B-V_{BE},\qquad
I_E\approx\frac{V_E}{R_E},\qquad
I_C\approx I_E
$$

The approximation $I_C\approx I_E$ is good when $\beta$ is sufficiently large.

### Voltage-divider bias

The base divider is replaced by its Thevenin equivalent:

$$
V_{TH}=V_{CC}\frac{R_2}{R_1+R_2},\qquad
R_{TH}=R_1\parallel R_2
$$

Including base loading:

$$
I_B\approx\frac{V_{TH}-V_{BE}}{R_{TH}+(\beta+1)R_E}
$$

Then $I_C\approx\beta I_B$ and $V_{CE}=V_{CC}-I_C R_C-I_E R_E$. A sufficiently stiff divider (divider current well above base current) reduces sensitivity to $\beta$.

### Collector-feedback bias

A resistor from collector to base provides feedback. If collector current increases, collector voltage falls, reducing base drive and counteracting the increase. This is generally more stable than fixed bias, though the operating point still depends on device parameters.

### Example: emitter-resistor voltage-divider bias

Given $V_{CC}=12$ V, $R_1=47\ \text{k}\Omega$, $R_2=10\ \text{k}\Omega$, $R_C=2.2\ \text{k}\Omega$, $R_E=1.0\ \text{k}\Omega$, $\beta=100$, and $V_{BE}=0.7$ V:

$$
V_{TH}=12\frac{10}{47+10}=2.105\ \text{V},\qquad
R_{TH}=47\parallel10=8.25\ \text{k}\Omega
$$

$$
I_B\approx\frac{2.105-0.7}{8.25\text{k}+101(1.0\text{k})}
=12.9\ \mu\text{A}
$$

$$
I_C\approx1.29\ \text{mA},\quad
I_E\approx1.30\ \text{mA},\quad
V_E\approx1.30\ \text{V}
$$

$$
V_{CE}\approx12-(1.29\text{mA})(2.2\text{k}\Omega)-1.30
\approx7.86\ \text{V}
$$

The Q-point is approximately $(I_C,V_{CE})=(1.29\ \text{mA},7.86\ \text{V})$, consistent with forward-active operation under the stated assumptions.

## 4. Bias stabilization

Transistor current changes with temperature and device variation. Stabilization aims to make the Q-point less sensitive to changes in $\beta$, $V_{BE}$, and leakage.

- Emitter-resistor feedback opposes current changes.
- Voltage-divider bias provides a relatively fixed base voltage.
- Thermal design must also keep transistor power within its safe operating limits.

No bias network removes all drift. Verify the Q-point across expected device and temperature variation for a practical design.

## 5. BJT amplifier AC analysis: the $r_e$ model

For a forward-active BJT at room temperature, the small-signal intrinsic emitter resistance is approximately:

$$
r_e\approx\frac{V_T}{I_E}\approx\frac{25.9\ \text{mV}}{I_E}
$$

where $I_E$ is the DC emitter current in amperes. For a bypassed-emitter CE stage with a load, a common midband approximation is:

$$
A_v\approx-\frac{R_C\parallel R_L}{r_e}
$$

The negative sign indicates inversion. This estimate assumes midband operation, a sufficiently large coupling/bypass capacitor, and neglect of transistor output resistance and other loading. Without emitter bypass, gain is reduced and linearity/stability may improve.

### Example: CE voltage gain

Let $I_E=1.0$ mA, $R_C=4.7\ \text{k}\Omega$, and $R_L=10\ \text{k}\Omega$:

$$
r_e\approx\frac{25.9\ \text{mV}}{1.0\ \text{mA}}=25.9\ \Omega
$$

$$
R_C\parallel R_L=4.7\text{k}\parallel10\text{k}=3.20\ \text{k}\Omega
$$

$$
A_v\approx-\frac{3.20\text{k}}{25.9}\approx-124
$$

The large-signal gain will be lower if the output swing is limited, emitter degeneration is present, or frequency-response effects matter.

## 6. Field-effect transistors (FETs)

FETs are voltage-controlled devices in which an electric field controls channel current. The gate draws very little DC current in normal operation; input resistance is therefore typically high. JFETs and MOSFETs differ in their gate construction and operating modes.

### JFET construction and characteristics

A JFET has a conductive channel between drain and source. A reverse-biased gate-channel junction changes the depletion width and narrows the channel. Increasing reverse gate-source voltage reduces drain current.

For an n-channel JFET in its saturation region, the Shockley transfer approximation is:

$$
I_D=I_{DSS}\left(1-\frac{V_{GS}}{V_P}\right)^2
$$

where $I_{DSS}$ is the zero-gate-bias saturation current and $V_P$ is the gate-source pinch-off voltage using the sign convention for that device. For an n-channel device, $V_P$ is normally negative. The relation is valid only over the model's specified region; consult the device data sheet for actual limits.

### Common-source (CS) amplifier

The CS configuration is the FET counterpart of a CE voltage amplifier: the source is common to input and output, and the output voltage is inverted. For a small-signal model:

$$
A_v\approx-g_m(R_D\parallel R_L)
$$

where $g_m$ is transconductance at the Q-point. Source degeneration reduces gain and improves bias stability.

### MOSFET types and transfer behavior

- **Depletion-mode MOSFET:** A physical channel exists at $V_{GS}=0$. Gate voltage can either deplete or enhance channel charge, depending on polarity and device type.
- **Enhancement-mode MOSFET:** No conducting channel exists at zero gate-source voltage. The appropriate gate polarity creates an inversion channel after threshold is reached.

For a long-channel enhancement NMOS in saturation, a simplified square-law model is:

$$
I_D\approx\frac{k_n}{2}(V_{GS}-V_{TH})^2,\qquad V_{GS}>V_{TH}
$$

where $k_n$ depends on device construction and $V_{TH}$ is threshold voltage. Real MOSFETs can depart significantly from this model; use the data sheet or a more detailed model for design.

### Example: JFET transfer current

An n-channel JFET has $I_{DSS}=8$ mA and $V_P=-4$ V. Estimate $I_D$ at $V_{GS}=-1$ V:

$$
I_D=8\left(1-\frac{-1}{-4}\right)^2
=8(0.75)^2=4.5\ \text{mA}
$$

The result is an idealized transfer-curve estimate; the drain-source voltage must also put the JFET in the region where the equation applies.

## 7. Review questions

1. Explain forward-active, cutoff, and saturation operation for an NPN BJT.
2. Relate $\alpha$ and $\beta$. If $\beta=99$, calculate $\alpha$.
3. Compare CB, CE, and CC configurations.
4. Why is fixed-base bias sensitive to temperature and transistor gain?
5. Calculate the Q-point for a fixed-bias CE circuit with stated component values.
6. What is the purpose of the emitter resistor in a bias network?
7. What does the negative sign in the CE gain equation indicate?
8. Find $r_e$ for $I_E=2$ mA at room temperature.
9. Explain how reverse gate bias controls JFET drain current.
10. Distinguish depletion-mode and enhancement-mode MOSFETs.
11. State the assumptions and limits of the JFET Shockley transfer equation.

## Further study

- [MIT OpenCourseWare 6.012 lecture notes](https://ocw.mit.edu/courses/6-012-microelectronic-devices-and-circuits-fall-2009/pages/lecture-notes/) — lectures 7–8 cover BJTs and LEDs; lectures 10–13 cover MOSFETs and small-signal models.
- [MIT OpenCourseWare 6.002 lecture notes](https://ocw.mit.edu/courses/6-002-circuits-and-electronics-spring-2007/pages/lecture-notes/) — MOSFET large-signal and small-signal amplifier notes.
- [OpenStax University Physics, Section 9.7: Semiconductor Devices](https://openstax.org/books/university-physics-volume-3/pages/9-7-semiconductor-devices) — semiconductor junctions and transistor overview.
- Boylestad and Nashelsky, *Electronic Devices and Circuit Theory* (listed in the course syllabus).
