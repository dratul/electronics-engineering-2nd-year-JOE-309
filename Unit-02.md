# Unit 02: Diode Applications and Special-Purpose Devices

This guide covers diode series/parallel circuits, rectifiers, clippers, clampers, Zener shunt regulators, voltage multipliers, LEDs, varactor diodes, tunnel diodes, and LCDs. Unless stated otherwise, numerical examples use the constant-voltage model and ideal components.

## Learning objectives

- Analyze simple diode networks using a stated ON/OFF model.
- Explain half-wave and full-wave rectification and calculate their basic output quantities.
- Distinguish clipping from clamping.
- Analyze a basic Zener shunt regulator and voltage multiplier.
- Describe the operating principle and common use of each special-purpose device.

## 1. Series, parallel, and series-parallel diode circuits

Diodes in a circuit do not automatically share voltage or current equally. First determine the applied polarity, then assume each diode is ON or OFF using an ideal or constant-drop model. Solve the resulting linear circuit and verify that the calculated diode voltage and current are consistent with the assumed state.

- **Series diodes:** In a conducting path, the same current passes through all diodes. Their forward drops add in a constant-drop model.
- **Parallel diodes:** Ideally, parallel diodes share voltage, but real forward-voltage differences can make one device carry more current. Current sharing may require ballast resistors or matched devices.
- **Series-parallel circuits:** Reduce the network one branch at a time, checking the bias of every diode after each assumption.

### Example: series diodes

A 5 V source drives two forward-biased silicon diodes and a 1 kΩ resistor in series. With $V_\gamma=0.7$ V per diode:

$$
I=\frac{5-2(0.7)}{1\,000}=3.6\ \text{mA}
$$

The assumed conducting state is consistent because the current is positive in the forward direction.

## 2. Rectifiers

A rectifier converts an alternating input into a unidirectional, pulsating output. A filter capacitor can reduce ripple, but the basic circuits below are considered without filtering unless noted.

### Half-wave rectifier

A single diode conducts during one half-cycle and blocks the other. For an ideal diode and a sinusoidal input with peak $V_m$:

- Output pulse frequency is the input frequency $f$.
- Average output voltage is $V_{DC}=V_m/\pi$.
- Peak inverse voltage (PIV) is approximately $V_m$.

With one constant-drop diode, a rough peak output estimate is $V_m-V_\gamma$; the exact average then depends on the source waveform and conduction interval.

### Full-wave rectifiers

Both half-cycles produce output of the same polarity, so the ripple frequency is $2f$.

1. **Center-tapped rectifier:** Uses two diodes and a center-tapped transformer. One diode conducts on each half-cycle. Each diode's approximate PIV is $2V_m$ when $V_m$ denotes the peak of one half of the secondary.
2. **Bridge rectifier:** Uses four diodes; two conduct in series during each half-cycle. It does not need a center-tapped secondary. Each nonconducting diode's PIV is approximately $V_m$, where $V_m$ is the peak across the full secondary.

For an ideal full-wave rectified sine:

$$
V_{DC}=\frac{2V_m}{\pi}\approx0.637V_m
$$

In a bridge, the peak output is approximately $V_m-2V_\gamma$ in the constant-drop model.

### Capacitor filter and ripple estimate

When a capacitor is placed across a resistive load, it charges near each peak and discharges into the load between peaks. For small ripple:

$$
V_{r(pp)}\approx\frac{I_L}{f_r C}
$$

where $f_r=f$ for a half-wave rectifier and $f_r=2f$ for a full-wave rectifier. This approximation assumes the ripple is small and the load current is approximately constant during a discharge interval.

### Example: bridge rectifier

A 12 V RMS transformer secondary feeds a bridge and a 1 kΩ load. Estimate peak output, average ideal full-wave output, and load current using $V_\gamma=0.7$ V per diode.

$$
V_m=12\sqrt{2}=16.97\ \text{V}
$$

Two diodes conduct at a time, so:

$$
V_{o(pk)}\approx16.97-2(0.7)=15.57\ \text{V}
$$

Using the ideal average formula as an approximation and accounting approximately for the bridge drop:

$$
V_{DC}\approx\frac{2V_m}{\pi}-1.4
=\frac{2(16.97)}{\pi}-1.4
\approx9.40\ \text{V}
$$

$$
I_L\approx\frac{9.40}{1\,000}=9.40\ \text{mA}
$$

This average estimate is approximate because the diode drop is not subtracted as a constant over the entire waveform.

## 3. Clippers

A **clipper** limits part of a waveform above or below a selected level without intentionally shifting the entire waveform's reference level.

- **Series clipper:** A diode is in series with the load; it passes one part of the input and blocks another.
- **Shunt clipper:** A diode is in parallel with the load; it diverts the selected part of the signal.
- **Biased clipper:** A DC source shifts the clipping threshold.
- **Combination clipper:** Oppositely oriented branches can limit both positive and negative peaks.

With a silicon diode and a DC bias, the practical threshold includes the diode's forward drop. Always state the diode orientation and source polarity when determining which half-cycle is clipped.

## 4. Clampers

A **clamper** shifts a waveform's DC level so one extreme is held near a reference. A basic clamper uses a diode, capacitor, and resistor.

- The diode conducts during the clamping interval and charges the capacitor.
- During the opposite interval, the diode is off and the capacitor approximately retains its charge.
- The output is the input plus the capacitor voltage, so the waveform is shifted rather than simply cut off.

For effective clamping, choose the time constant $RC$ much larger than the input period $T$. A practical diode drop shifts the clamp level away from the ideal reference.

## 5. Zener diode as a shunt regulator

A reverse-biased Zener is connected in parallel with the load. A series resistor limits current from the supply. When the Zener operates within its specified breakdown-current range, the load voltage is approximately $V_Z$.

$$
I_S=\frac{V_S-V_Z}{R_S},\qquad
I_L=\frac{V_Z}{R_L},\qquad
I_Z=I_S-I_L
$$

Check both extremes:

- At maximum load current and minimum supply, make sure $I_Z$ remains at or above the specified knee/regulation current.
- At minimum load current and maximum supply, check that Zener current and power do not exceed ratings.
- Resistor power is $P_R=I_S^2R_S$.

### Example: choosing a shunt resistor

A 12 V source feeds a 5.1 V Zener regulator and a 1 kΩ load. For $R_S=330\ \Omega$:

$$
I_L=\frac{5.1}{1\,000}=5.1\ \text{mA}
$$

$$
I_S=\frac{12-5.1}{330}=20.9\ \text{mA},\qquad
I_Z=20.9-5.1=15.8\ \text{mA}
$$

$$
P_Z=V_ZI_Z\approx5.1(0.0158)=81\ \text{mW}
$$

The result is valid only if the Zener's minimum and maximum current limits, power rating, resistor rating, and supply/load variations are all satisfied.

## 6. Voltage-multiplier circuits

Voltage multipliers use diodes and capacitors to charge capacitors on alternating half-cycles and add their voltages in series. A voltage doubler ideally produces a no-load output near $2V_m$; a tripler and higher multiplier use additional diode-capacitor stages.

Actual output is lower because of diode drops, capacitor leakage, load current, and ripple. As the number of stages increases, output regulation generally worsens and the output becomes more sensitive to load. Multipliers are useful where high voltage is needed at relatively low current.

## 7. Special-purpose two-terminal devices

### Light-emitting diode (LED)

An LED emits light when forward-biased carriers recombine radiatively. Its color depends mainly on the semiconductor bandgap. Like other diodes, an LED requires current limiting.

$$
R=\frac{V_S-V_F}{I_F}
$$

**Example:** For a 5 V source, $V_F=2.0$ V, and target current $I_F=10$ mA:

$$
R=\frac{5-2}{0.010}=300\ \Omega
$$

Choose a standard value at or above this value if the design must not exceed the target current, then verify LED and resistor power ratings.

### Varactor (varicap) diode

A varactor is operated in reverse bias. Its depletion-layer capacitance changes with reverse voltage, so it acts as a voltage-controlled capacitor. It is used in tuned RF circuits and electronic frequency tuning. It should not be driven into forward conduction during normal operation.

### Tunnel diode

A tunnel diode is very heavily doped, making its depletion region extremely narrow. Quantum tunneling creates a region in its I-V curve where increasing voltage causes current to decrease; this is **negative differential resistance**. It can be used in specialized high-frequency oscillators and switching circuits.

### Liquid-crystal display (LCD)

An LCD controls the passage or polarization of light by changing the orientation of liquid-crystal molecules with an applied electric field. The display is not a light source, so it usually requires ambient or backlight illumination. AC drive is commonly used to avoid sustained DC across the liquid crystal, which can degrade the display.

## 8. Review questions

1. Compare half-wave, center-tapped full-wave, and bridge rectifiers.
2. A 50 Hz source drives a full-wave rectifier. What is the ripple frequency before filtering?
3. Explain why a bridge has two conducting diode drops in each half-cycle.
4. How does a capacitor filter reduce rectifier ripple? State the assumptions behind the small-ripple formula.
5. Distinguish a clipper from a clamper.
6. A 9 V supply drives a 3.3 V LED at 15 mA. Find the series resistor and its approximate dissipation.
7. Explain why a Zener shunt regulator needs a series resistor.
8. Describe the principle of a voltage doubler.
9. Why is a varactor operated in reverse bias?
10. What is negative differential resistance in a tunnel diode?
11. Why does an LCD normally need ambient light or a backlight?

## Further study

- [OpenStax University Physics, Section 9.7: Semiconductor Devices](https://openstax.org/books/university-physics-volume-3/pages/9-7-semiconductor-devices) — PN junction behavior, semiconductor devices, and LEDs.
- [MIT OpenCourseWare 6.012 lecture notes](https://ocw.mit.edu/courses/6-012-microelectronic-devices-and-circuits-fall-2009/pages/lecture-notes/) — semiconductor devices and LED lecture material.
- Boylestad and Nashelsky, *Electronic Devices and Circuit Theory* — rectifiers, clipping/clamping, Zener regulation, and special-purpose diodes (listed in the course syllabus).
