# 7. Diode equivalent circuits

**Author:** Dr. Atul Kumar Dwivedi

An equivalent circuit replaces the diode with a simpler model to make circuit calculations manageable.

1. **Ideal model:** Treat an ON diode as a short and an OFF diode as an open.
2. **Constant-voltage model:** When ON, use a fixed forward drop; when OFF, use an open circuit.
3. **Piecewise-linear model:** When ON, use a fixed drop in series with a resistance; when OFF, use an open circuit.

For any model, first make a reasonable ON/OFF assumption, analyze the circuit, and then check that the resulting diode voltage and current agree with that assumption.

## Short example: series resistor and silicon diode

A 5 V source drives a silicon diode and a 1 kΩ resistor in series. Using the constant-drop model $V_\gamma=0.7$ V, with the diode forward biased:

$$
I_D \approx \frac{5-0.7}{1\,000}=4.3\ \text{mA}
$$

The resistor limits the current; the diode alone does not set a safe current.

## Navigation

- **Next topic:** [Zener and avalanche breakdown](08-zener-and-avalanche-breakdown.md)
- **Related topics:** [Ideal and practical diode models](04-ideal-and-practical-diode-models.md), [Diode resistance](05-diode-resistance.md), [Zener and avalanche breakdown](08-zener-and-avalanche-breakdown.md), [Worked examples](09-worked-examples.md)
- [Back to Unit I index](readme.md)
