# Unit 04: Operational Amplifiers

This guide covers op-amp fundamentals and practical limitations, differential and common-mode signals, inverting and non-inverting amplifiers, voltage follower, summing amplifier, integrator, differentiator, and input/output offset and bias-current parameters.

## Learning objectives

- Apply the ideal op-amp rules when negative feedback is present.
- Calculate gain and output for common op-amp circuits.
- Explain differential and common-mode signals and CMRR.
- Identify how offset voltage and input currents affect practical circuits.
- Recognize output swing, bandwidth, slew-rate, and input-range limitations.

## 1. Op-amp basics

An operational amplifier is a high-gain differential voltage amplifier. Its output responds to the difference between its non-inverting and inverting inputs:

$$
V_O=A_{OL}(V_+-V_-)
$$

where $A_{OL}$ is the open-loop gain. In open loop, even a small input difference usually drives the output toward a supply rail. Most linear applications use negative feedback.

### Ideal model and negative feedback

For an ideal op-amp operating linearly with negative feedback:

1. Input currents are zero: $I_+=I_-=0$.
2. The input voltages are equal: $V_+\approx V_-$ (virtual short).
3. The output is not necessarily at ground; a virtual ground exists only when feedback holds an input at ground potential.

These rules are approximations for analysis. They do not apply when the output is saturated, the feedback is positive, or the input common-mode range is exceeded.

## 2. Differential and common-mode operation

The differential input is the difference of the two input voltages:

$$
V_D=V_+-V_-
$$

The common-mode input is their average:

$$
V_{CM}=\frac{V_++V_-}{2}
$$

A practical op-amp amplifies the differential component and ideally rejects the common-mode component. Its common-mode rejection ratio is:

$$
\text{CMRR}=\left|\frac{A_D}{A_{CM}}\right|,\qquad
\text{CMRR}_{dB}=20\log_{10}(\text{CMRR})
$$

Higher CMRR means better rejection of signals common to both inputs, subject to frequency and operating-condition limits.

### Differential amplifier circuit

A four-resistor difference amplifier subtracts two input voltages. If the resistor ratios are matched so that $R_2/R_1=R_4/R_3$, then:

$$
V_O=\frac{R_2}{R_1}(V_2-V_1)
$$

The resistor-ratio matching is important: mismatch reduces common-mode rejection. The op-amp inputs must also remain within their common-mode range.

**Example:** For matched ratios $R_2/R_1=R_4/R_3=10$ and inputs $V_2=0.30$ V, $V_1=0.10$ V:

$$
V_O=10(0.30-0.10)=2.0\ \text{V}
$$

## 3. Practical characteristics and parameters

Real op-amps have finite open-loop gain and bandwidth, nonzero input currents, offset voltage, finite output drive, and limited input/output voltage ranges. Check the data sheet for the exact part.

- **Input offset voltage $V_{OS}$:** Small differential input voltage required to make the output zero under specified conditions.
- **Input bias current $I_B$:** Average current flowing into (or out of) the two input terminals.
- **Input offset current $I_{OS}$:** Difference between the two input bias currents.
- **Output offset voltage:** Output voltage error caused by input offsets and circuit gains when the intended signal is zero.
- **Input common-mode range:** Allowed voltage range at the input terminals for correct operation.
- **Output swing:** Maximum output range under the specified load; usually short of the supply rails unless the part is rail-to-rail.
- **Gain-bandwidth product:** For a simple dominant-pole op-amp, closed-loop bandwidth decreases as closed-loop gain increases.
- **Slew rate:** Maximum rate of change of output voltage, limiting large, fast signals.

For a sine-wave output of peak amplitude $V_P$ and frequency $f$, the required peak slew rate is:

$$
\text{SR}_{required}=2\pi f V_P
$$

### Example: slew-rate limit

An op-amp must produce a 5 V peak, 20 kHz sine wave. The required slew rate is:

$$
\text{SR}=2\pi(20\,000)(5)
=628\,319\ \text{V/s}
\approx0.628\ \text{V}/\mu\text{s}
$$

Choose an op-amp with a slew rate above this value, with margin, and also check bandwidth and output swing.

## 4. Inverting amplifier

Connect the non-inverting input to ground, the signal to the inverting input through $R_{in}$, and feedback resistor $R_f$ from output to the inverting input. For an ideal op-amp with negative feedback:

$$
A_V=\frac{V_O}{V_{in}}=-\frac{R_f}{R_{in}}
$$

The minus sign indicates a 180-degree phase inversion.

### Example

For $R_{in}=10\ \text{k}\Omega$, $R_f=47\ \text{k}\Omega$, and $V_{in}=0.20$ V:

$$
V_O=-\frac{47}{10}(0.20)=-0.94\ \text{V}
$$

This result is valid only if the supply rails, output-load capability, and input/output ranges permit $-0.94$ V.

## 5. Non-inverting amplifier and voltage follower

Apply the signal to the non-inverting input and use a resistor divider from output to the inverting input:

$$
A_V=1+\frac{R_f}{R_g}
$$

The output is in phase with the input. A voltage follower connects output directly to the inverting input and has ideal gain 1. It provides high input resistance and low output resistance within the op-amp's limits.

### Example

With $R_f=30\ \text{k}\Omega$, $R_g=10\ \text{k}\Omega$, and $V_{in}=0.25$ V:

$$
A_V=1+\frac{30}{10}=4,\qquad V_O=4(0.25)=1.0\ \text{V}
$$

## 6. Summing amplifier

An inverting summing amplifier combines multiple input currents at the virtual-ground node:

$$
V_O=-R_f\left(\frac{V_1}{R_1}+\frac{V_2}{R_2}+\cdots\right)
$$

Equal input resistors give a scaled, inverted sum. Unequal resistors give each input a different weight. Check that the calculated output remains within the available output swing.

### Example

For $R_f=20\ \text{k}\Omega$, $R_1=10\ \text{k}\Omega$, $R_2=20\ \text{k}\Omega$, $V_1=0.5$ V, and $V_2=1.0$ V:

$$
V_O=-20\text{k}\left(\frac{0.5}{10\text{k}}+\frac{1.0}{20\text{k}}\right)
=-2.0\ \text{V}
$$

## 7. Integrator and differentiator

### Inverting integrator

Replace the feedback resistor with a capacitor $C_f$. With an input resistor $R$:

$$
V_O(t)=-\frac{1}{RC_f}\int V_{in}(t)\,dt+V_O(t_0)
$$

For a constant input $V_{in}$ over time $\Delta t$, the ideal output change is:

$$
\Delta V_O=-\frac{V_{in}\Delta t}{RC_f}
$$

Practical integrators commonly add a resistor in parallel with the capacitor to limit DC gain and prevent offset-driven saturation.

### Inverting differentiator

With an input capacitor $C$ and feedback resistor $R_f$:

$$
V_O=-R_f C\frac{dV_{in}}{dt}
$$

An ideal differentiator strongly amplifies high-frequency noise. Practical circuits add components to limit the bandwidth and improve stability.

### Example: integrator ramp

An integrator uses $R=100\ \text{k}\Omega$ and $C_f=0.1\ \mu\text{F}$. A constant $0.20$ V input is applied for 10 ms:

$$
\Delta V_O=-\frac{(0.20)(0.010)}
{(100\,000)(0.1\times10^{-6})}
=-0.20\ \text{V}
$$

This assumes the op-amp starts in its linear range and the output does not saturate.

## 8. Offset and bias-current effects

Input offset voltage is amplified by the circuit's noise gain. Input bias currents flowing through source and feedback resistances create additional voltage errors. For an inverting amplifier, a compensation resistor at the non-inverting input is sometimes chosen as:

$$
R_{comp}=R_{in}\parallel R_f
$$

This can reduce error from matched input bias currents, but it does not remove input offset voltage, offset-current error, or all temperature effects. Use the actual amplifier data sheet and error budget for precision work.

### Example: offset contribution

If an op-amp has $V_{OS}=2$ mV and the circuit's noise gain is 11, the approximate output offset contribution from $V_{OS}$ is:

$$
V_{O,OS}\approx 11(2\ \text{mV})=22\ \text{mV}
$$

Other sources of offset may add to this error.

## 9. Review questions

1. State the two ideal op-amp rules used for a linear negative-feedback circuit.
2. Why does an op-amp in open loop usually saturate?
3. Find the gain of an inverting amplifier with $R_f=100\ \text{k}\Omega$ and $R_{in}=20\ \text{k}\Omega$.
4. Find the gain of a non-inverting amplifier with $R_f=39\ \text{k}\Omega$ and $R_g=10\ \text{k}\Omega$.
5. Calculate the output of a two-input summing amplifier for given values.
6. How does a constant input appear at the output of an ideal integrator?
7. Why is a practical differentiator bandwidth-limited?
8. Define input bias current and input offset current.
9. Calculate the CMRR in dB if $A_D/A_{CM}=10^4$.
10. What data-sheet limits must be checked before accepting an ideal gain calculation?

## Further study

- [Texas Instruments: Op-amp application notes and design resources](https://www.ti.com/amplifier-circuit/op-amps/overview.html) — consult the device data sheet and application notes for real input/output limits, stability, and offset behavior.
- Boylestad and Nashelsky, *Electronic Devices and Circuit Theory* — op-amp fundamentals and circuits (listed in the course syllabus).
- H. S. Kalsi, *Electronic Instrumentation* — measurement and instrumentation references (listed in the course syllabus).
