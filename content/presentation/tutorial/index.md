+++
title = "Technical Deep Dive"
date = 2026-01-11
description = "A deep dive into our new architecture."
theme="serif"
math_engine="KaTeX"
+++

# Slide 1

Welcome to the deck.

---

# Slide 2

Horizontal split.

===

# Slide 2.1

Vertical split.

---

## The Lorenz Equations $\mu$

$$
\begin{aligned}
    \dot{x} & = \sigma(y-x) \\
    \dot{y} & = \rho x - y - xz \\
    \dot{z} & = -\beta z + xy \\
    \dfrac{1}{2} & = 0.5
\end{aligned}
$$

---

## Code block

{{< code language="python" line_number=true >}}
import numpy as np
print("Hello World")
{{< /code >}}
