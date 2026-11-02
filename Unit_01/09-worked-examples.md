# 9. Worked examples and review

## Example 1: Diode current from the Shockley equation

At room temperature, estimate the current for a diode with $I_S=2\ \text{nA}$, $\eta=2$, and $V_D=0.60\ \text{V}$. Ignore series resistance.

Using $V_T=25.9\ \text{mV}$:

$$
\begin{aligned}
I_D &= I_S\left(e^{V_D/(\eta V_T)}-1\right)\\
&=2\times10^{-9}\left(e^{0.60/(2\times0.0259)}-1\right)\\
&\approx 0.214\ \text{mA}
\end{aligned}
$$

The exponential model predicts a current of approximately $214\ \mu\text{A}$. A real circuit's series resistance and source impedance may change the actual current.

## Example 2: DC and small-signal resistance

A diode is biased at $V_D=0.62\ \text{V}$ and $I_D=4.0\ \text{mA}$. Find its DC resistance and estimate its small-signal resistance at room temperature, assuming $\eta=1$.

$$
R_D=\frac{V_D}{I_D}=\frac{0.62}{0.004}=155\ \Omega
$$

$$
r_d\approx\frac{\eta V_T}{I_D}
=\frac{25.9\ \text{mV}}{4.0\ \text{mA}}
\approx6.48\ \Omega
$$

The values differ because $R_D$ is the voltage-to-current ratio at the operating point, while $r_d$ is the local small-signal slope.

## Example 3: Estimate transition capacitance

Approximate a reverse-biased silicon junction as a parallel-plate capacitor. Let $\epsilon_r=11.7$, junction area $A=1.0\ \text{mm}^2$, and depletion width $W=2.0\ \mu\text{m}$. Use $\epsilon_0=8.854\times10^{-12}\ \text{F/m}$.

Convert the dimensions:

$$
A=1.0\times10^{-6}\ \text{m}^2,\qquad
W=2.0\times10^{-6}\ \text{m}
$$

Then:

$$
\begin{aligned}
C_T&\approx\frac{\epsilon_r\epsilon_0 A}{W}\\
&=\frac{(11.7)(8.854\times10^{-12})(1.0\times10^{-6})}
{2.0\times10^{-6}}\\
&\approx 5.18\times10^{-11}\ \text{F}
=51.8\ \text{pF}
\end{aligned}
$$

This is an idealized estimate; an actual junction's geometry and doping profile affect its capacitance.

## Example 4: Zener shunt regulator with a load

A $12\ \text{V}$ supply feeds a $5.1\ \text{V}$ Zener regulator through $R_S=330\ \Omega$. The load is $R_L=1.0\ \text{k}\Omega$. Assuming the Zener holds $V_Z=5.1\ \text{V}$, calculate the load current, series current, Zener current, and Zener power. Check that the Zener current is at least $5\ \text{mA}$ for regulation.

Load current:

$$
I_L=\frac{V_Z}{R_L}=\frac{5.1}{1000}=5.1\ \text{mA}
$$

Current through the series resistor:

$$
I_S=\frac{V_S-V_Z}{R_S}
=\frac{12-5.1}{330}
\approx20.9\ \text{mA}
$$

By Kirchhoff's current law, the remaining current flows through the Zener:

$$
I_Z=I_S-I_L=20.9-5.1=15.8\ \text{mA}
$$

Since $15.8\ \text{mA}>5\ \text{mA}$, the stated minimum-current condition is met. Zener power is:

$$
P_Z=V_ZI_Z=(5.1)(0.0158)\approx0.081\ \text{W}
$$

The series resistor also dissipates power:

$$
P_{R_S}=(V_S-V_Z)I_S=(6.9)(0.0209)\approx0.144\ \text{W}
$$

Choose a Zener with a power rating comfortably above $81\ \text{mW}$ and a resistor rated above $0.144\ \text{W}$ (for example, $0.25\ \text{W}$ with appropriate derating). Also check the Zener's maximum current and worst-case component tolerances in a real design.

## Formula and concept review

| Quantity | Relation or key idea |
|---|---|
| Thermal voltage | $V_T=kT/q$, approximately 25.9 mV at room temperature |
| Diode equation | $I_D=I_S(e^{V_D/(\eta V_T)}-1)$ |
| DC resistance | $R_D=V_D/I_D$ at the operating point |
| Small-signal resistance | $r_d\approx\eta V_T/I_D$ for forward bias |
| Transition capacitance | $C_T\approx\epsilon A/W$; usually decreases as reverse bias increases |
| Diffusion capacitance | $C_D=dQ/dV_D$; associated with stored injected charge in forward bias |

## Self-test questions

1. What distinguishes intrinsic from extrinsic semiconductor material?
2. Identify the majority and minority carriers in N-type and P-type material.
3. Explain how diffusion creates a depletion region and built-in electric field.
4. Describe what happens to the depletion width in forward and reverse bias.
5. Sketch and label the forward, reverse-leakage, and breakdown regions of a diode V-I characteristic.
6. Compare the ideal, constant-voltage, and piecewise-linear diode models.
7. A diode has $V_D=0.68$ V and $I_D=10$ mA. Find its DC resistance.
8. Estimate $r_d$ at room temperature for $I_D=5$ mA and $\eta=1$.
9. Why is transition capacitance most significant in reverse bias?
10. Explain the difference between Zener and avalanche breakdown.

### Answers to calculation checks

- **Question 7:** $R_D=0.68/0.010=68\ \Omega$.
- **Question 8:** $r_d\approx25.9\ \text{mV}/5\ \text{mA}\approx5.18\ \Omega$.

## Study tips

- Practice drawing the diode symbol and labeling anode, cathode, $V_D$, and $I_D$.
- On V-I graphs, label the forward knee, reverse leakage, and breakdown voltage/current direction.
- Keep static resistance $V_D/I_D$ separate from small-signal resistance $\eta V_T/I_D$.
- For each diode circuit problem, state the chosen model and verify the assumed ON/OFF state.
- Remember that approximate silicon and germanium forward drops are model values, not universal constants.

## Further study

- [OpenStax University Physics, Section 9.6: Semiconductors and Doping](https://openstax.org/books/university-physics-volume-3/pages/9-6-semiconductors-and-doping) — semiconductor doping and carrier types.
- [OpenStax University Physics, Section 9.7: Semiconductor Devices](https://openstax.org/books/university-physics-volume-3/pages/9-7-semiconductor-devices) — PN junction formation, forward/reverse bias, and diode behavior.
- [MIT OpenCourseWare 6.012 lecture notes](https://ocw.mit.edu/courses/6-012-microelectronic-devices-and-circuits-fall-2009/pages/lecture-notes/) — semiconductor and PN-junction lectures.
- Boylestad and Nashelsky, *Electronic Devices and Circuit Theory* (listed in the course syllabus).

## Navigation

- **Next topic:** [Back to Unit I index](readme.md)
- **Related topics:** [Biasing and V-I characteristics](03-biasing-and-vi-characteristics.md), [Diode resistance](05-diode-resistance.md), [Junction capacitances](06-junction-capacitances.md), [Zener and avalanche breakdown](08-zener-and-avalanche-breakdown.md)
- [Back to Unit I index](readme.md)
