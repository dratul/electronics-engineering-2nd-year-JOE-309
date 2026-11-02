# 5. Diode resistance

**Author:** Dr. Atul Kumar Dwivedi

## DC (static) resistance

At a particular operating point, the ratio of diode voltage to diode current is

$$
R_D = \frac{V_D}{I_D}.
$$

This is the slope of a line from the origin to the operating point on the V-I graph.

## AC (dynamic or small-signal) resistance

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

## Navigation

- **Next topic:** [Junction capacitances](06-junction-capacitances.md)
- **Related topics:** [Biasing and V-I characteristics](03-biasing-and-vi-characteristics.md), [Ideal and practical diode models](04-ideal-and-practical-diode-models.md), [Junction capacitances](06-junction-capacitances.md), [Worked examples](09-worked-examples.md)
- [Back to Unit I index](readme.md)
