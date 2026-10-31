# Unit 01: Semiconductor Diode

This guide covers the Unit I syllabus: semiconductor materials, the PN junction, diode characteristics and models, diode resistance and capacitance, and Zener and avalanche breakdown.

## Learning objectives

After studying this unit, you should be able to:

- Distinguish intrinsic and extrinsic semiconductors and identify their majority carriers.
- Explain how a PN junction and depletion region form.
- Interpret forward- and reverse-bias V-I characteristics.
- Use ideal, constant-voltage, and piecewise-linear diode models.
- Calculate static and small-signal diode resistance.
- Explain transition and diffusion capacitance.
- Distinguish Zener breakdown from avalanche breakdown.

## 1. Semiconductor materials

A semiconductor has electrical conductivity between that of a conductor and an insulator. Silicon and germanium are common semiconductor materials. Their conductivity depends on temperature, illumination, and the concentration of intentionally added impurities.

### Intrinsic and extrinsic materials

- **Intrinsic semiconductor:** A chemically pure semiconductor. Thermal energy can create electron-hole pairs; in an intrinsic material, the electron and hole concentrations are equal.
- **Extrinsic semiconductor:** A semiconductor whose conductivity has been increased by doping it with a controlled amount of impurity.
  - **N-type:** Doped with donor atoms, commonly pentavalent atoms such as phosphorus. Electrons are the majority carriers; holes are the minority carriers.
  - **P-type:** Doped with acceptor atoms, commonly trivalent atoms such as boron. Holes are the majority carriers; electrons are the minority carriers.

Doping does not give the material a net charge. It increases the concentration of mobile carriers. In a semiconductor, conductivity generally increases with temperature because more electron-hole pairs are generated.

## 2. PN junction and depletion region

A PN junction is the boundary between P-type and N-type regions in a single semiconductor crystal. When the junction is formed:

1. Electrons diffuse from the N side toward the P side, while holes diffuse from the P side toward the N side.
2. Electrons and holes recombine near the boundary.
3. This leaves fixed, ionized donor and acceptor atoms near the junction, creating a region depleted of mobile carriers.
4. The fixed charges create an electric field and a built-in potential that oppose further diffusion.

This carrier-depleted area is called the **depletion region** or **depletion layer**. The built-in potential is sometimes called the barrier potential. It is not a fixed forward-voltage drop under every operating condition: typical room-temperature approximations for silicon and germanium are about 0.7 V and 0.3 V, respectively.

## 3. Biasing and V-I characteristics

Let $V_D$ be the voltage from the diode anode (P side) to cathode (N side), and let $I_D$ be positive in the forward direction.

### Forward bias

Connect the P side to the more positive supply terminal and the N side to the more negative terminal. The applied field opposes the junction field, reducing the depletion width and barrier. A substantial current flows once the applied voltage is sufficient; the familiar 0.7 V (silicon) and 0.3 V (germanium) values are useful circuit approximations, not exact switching thresholds.

### Reverse bias

Connect the P side to the more negative supply terminal and the N side to the more positive terminal. The applied field reinforces the junction field, widening the depletion region. Only a small reverse current normally flows, mainly due to minority carriers, until breakdown is reached.

### Characteristic regions

- **Forward region:** Current rises rapidly with forward voltage.
- **Reverse leakage region:** A small reverse current flows before breakdown.
- **Breakdown region:** Reverse current rises sharply. A conventional diode may be damaged if the current is not limited. A suitably designed Zener diode can operate here within its ratings.

The idealized diode current-voltage relation is the Shockley equation:

$$
I_D = I_S\left(e^{V_D/(\eta V_T)}-1\right)
$$

where $I_S$ is the reverse saturation current, $\eta$ is the ideality factor (typically between 1 and 2), and $V_T=kT/q$ is the thermal voltage. At room temperature, $V_T$ is approximately 25.9 mV. The equation is a useful model, but real devices have limits such as series resistance and breakdown.

## 4. Ideal and practical diode models

The model chosen depends on the accuracy needed for the circuit analysis.

| Model | Forward-biased approximation | Reverse-biased approximation |
|---|---|---|
| Ideal | Short circuit; zero voltage drop | Open circuit; zero current |
| Constant-voltage-drop | Fixed drop $V_\gamma$, often about 0.7 V for silicon | Open circuit |
| Piecewise-linear | $V_\gamma$ in series with a small resistance $r_d$ | Open circuit, below breakdown |

An ideal diode is a mathematical simplification. A practical diode has a nonzero forward voltage, finite resistance, and a small reverse leakage current. The constant-voltage model is often sufficient for hand analysis; include $r_d$ when the change in voltage with current matters.

## 5. Diode resistance

### DC (static) resistance

At a particular operating point, the ratio of diode voltage to diode current is

$$
R_D = \frac{V_D}{I_D}.
$$

This is the slope of a line from the origin to the operating point on the V-I graph.

### AC (dynamic or small-signal) resistance

For a small change around a forward-biased operating point $Q$, the dynamic resistance is the local slope:

$$
r_d = \left.\frac{dV_D}{dI_D}\right|_Q
\approx \frac{\eta V_T}{I_D}
$$

Use amperes for $I_D$. For example, at room temperature with $\eta=1$ and $I_D=2\ \text{mA}$:

$$
r_d \approx \frac{25.9\ \text{mV}}{2\ \text{mA}} \approx 13\ \Omega
$$

This is a small-signal approximation, not the DC ratio $V_D/I_D$. In general, forward dynamic resistance decreases as the bias current increases.

## 6. Junction capacitances

A diode's capacitance is important when signals change quickly or when a circuit operates at high frequency.

### Transition (depletion) capacitance

Transition capacitance is most significant under reverse bias. The depletion region acts approximately like the insulating spacing between the charges on a capacitor's plates. For a simple parallel-plate picture:

$$
C_T \approx \frac{\epsilon A}{W}
$$

where $\epsilon$ is the semiconductor permittivity, $A$ is junction area, and $W$ is depletion width. Increasing reverse bias generally widens $W$, so $C_T$ decreases.

### Diffusion capacitance

Diffusion capacitance is most significant under forward bias. It results from stored injected minority-carrier charge in the regions next to the junction. In a simple charge-control model:

$$
C_D = \frac{dQ}{dV_D}
$$

where $Q$ is the stored charge. It generally increases with forward current and can affect switching speed.

## 7. Diode equivalent circuits

An equivalent circuit replaces the diode with a simpler model to make circuit calculations manageable.

1. **Ideal model:** Treat an ON diode as a short and an OFF diode as an open.
2. **Constant-voltage model:** When ON, use a fixed forward drop; when OFF, use an open circuit.
3. **Piecewise-linear model:** When ON, use a fixed drop in series with a resistance; when OFF, use an open circuit.

For any model, first make a reasonable ON/OFF assumption, analyze the circuit, and then check that the resulting diode voltage and current agree with that assumption.

### Short example: series resistor and silicon diode

A 5 V source drives a silicon diode and a 1 kΩ resistor in series. Using the constant-drop model $V_\gamma=0.7$ V, with the diode forward biased:

$$
I_D \approx \frac{5-0.7}{1\,000}=4.3\ \text{mA}
$$

The resistor limits the current; the diode alone does not set a safe current.

## 8. Zener and avalanche breakdown

Both mechanisms cause a large increase in reverse current. The reverse current must be limited by the surrounding circuit.

### Zener breakdown

Zener breakdown is associated with a very strong electric field in a heavily doped junction with a narrow depletion region. The field enables carriers to cross the junction by quantum-mechanical tunneling. It is usually dominant at relatively low breakdown voltages.

### Avalanche breakdown

Avalanche breakdown is associated with impact ionization. In a more lightly doped junction with a wider depletion region, carriers accelerated by the field collide with atoms and generate additional electron-hole pairs. This carrier multiplication can produce a large reverse current and is usually dominant at higher breakdown voltages.

The terms describe dominant mechanisms; both can contribute near a device's breakdown voltage. A Zener diode is designed to operate in reverse breakdown over its specified current and power range. With a suitable current-limiting circuit, it can provide a reference voltage or basic shunt regulation.

| Feature | Zener-dominant breakdown | Avalanche-dominant breakdown |
|---|---|---|
| Main mechanism | Strong-field tunneling | Impact ionization and carrier multiplication |
| Typical junction doping | Heavier | Lighter |
| Depletion region | Narrower | Wider |
| Typical breakdown voltage | Lower | Higher |

## 9. Formula and concept review

| Quantity | Relation or key idea |
|---|---|
| Thermal voltage | $V_T=kT/q$, approximately 25.9 mV at room temperature |
| Diode equation | $I_D=I_S(e^{V_D/(\eta V_T)}-1)$ |
| DC resistance | $R_D=V_D/I_D$ at the operating point |
| Small-signal resistance | $r_d\approx\eta V_T/I_D$ for forward bias |
| Transition capacitance | $C_T\approx\epsilon A/W$; usually decreases as reverse bias increases |
| Diffusion capacitance | $C_D=dQ/dV_D$; associated with stored injected charge in forward bias |

## 10. Self-test questions

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
