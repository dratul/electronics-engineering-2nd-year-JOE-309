# 6. Junction capacitances

A diode's capacitance is important when signals change quickly or when a circuit operates at high frequency.

## Transition (depletion) capacitance

Transition capacitance is most significant under reverse bias. The depletion region acts approximately like the insulating spacing between the charges on a capacitor's plates. For a simple parallel-plate picture:

$$
C_T \approx \frac{\epsilon A}{W}
$$

where $\epsilon$ is the semiconductor permittivity, $A$ is junction area, and $W$ is depletion width. Increasing reverse bias generally widens $W$, so $C_T$ decreases.

## Diffusion capacitance

Diffusion capacitance is most significant under forward bias. It results from stored injected minority-carrier charge in the regions next to the junction. In a simple charge-control model:

$$
C_D = \frac{dQ}{dV_D}
$$

where $Q$ is the stored charge. It generally increases with forward current and can affect switching speed.

## Navigation

- **Next topic:** [Diode equivalent circuits](07-diode-equivalent-circuits.md)
- **Related topics:** [PN junction and depletion region](02-pn-junction-and-depletion-region.md), [Biasing and V-I characteristics](03-biasing-and-vi-characteristics.md), [Diode resistance](05-diode-resistance.md), [Worked examples](09-worked-examples.md)
- [Back to Unit I index](../Unit-01.md)
