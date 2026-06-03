+++
title = "Technical Deep Dive"
date = 2026-01-11
description = "A deep dive into our new architecture."
theme="serif"
math_engine="KaTeX"
code_theme="xt256"
+++

# Slide 1

<!-- .slide: data-background="#ff0000" -->

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

{{< code language="python" line_number=true start_from=7 >}}
import numpy as np

print("Hello World")
{{< /code >}}

---

# The most stoopid dog ever?

===

<img src="./img/golden_retriever.jpeg" width="50%" alt="Golden retriever">

===

## Poupouille!

---

# QR Code


{{< qr text="https://gohugo.io" scale=10 />}}

---

# Molstar

{{< 
    molstar
        loadPdb="7SGL 5EWE"
        loadAlphafold="Q8W3K0"
        structureUrl="https://files.rcsb.org/view/9UYV.pdb pdb ; https://files.rcsb.org/view/9VKI.pdb pdb"
>}}

===

# Mouais…

{{< 
    molstar
        transparent="false"
        structureUrl="./static/2ESJ.pdb pdb"
        volumeUrl="./static/2ESJ_pi_stacking.mrc ccp4 true"
>}}

===

# MVSJ

{{<
    molstar
        structureUrl="./static/9i38.pdb pdb"
        mvsjUrl="./static/visualization.mvsj"
>}}
