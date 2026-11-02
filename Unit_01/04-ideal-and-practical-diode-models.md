# 4. Ideal and practical diode models

The model chosen depends on the accuracy needed for the circuit analysis.

| Model | Forward-biased approximation | Reverse-biased approximation |
|---|---|---|
| Ideal | Short circuit; zero voltage drop | Open circuit; zero current |
| Constant-voltage-drop | Fixed drop $V_\gamma$, often about 0.7 V for silicon | Open circuit |
| Piecewise-linear | $V_\gamma$ in series with a small resistance $r_d$ | Open circuit, below breakdown |

An ideal diode is a mathematical simplification. A practical diode has a nonzero forward voltage, finite resistance, and a small reverse leakage current. The constant-voltage model is often sufficient for hand analysis; include $r_d$ when the change in voltage with current matters.

## Navigation

- **Next topic:** [Diode resistance](05-diode-resistance.md)
- **Related topics:** [Biasing and V-I characteristics](03-biasing-and-vi-characteristics.md), [Diode resistance](05-diode-resistance.md), [Diode equivalent circuits](07-diode-equivalent-circuits.md), [Worked examples](09-worked-examples.md)
- [Back to Unit I index](readme.md)
