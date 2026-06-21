+++
title = "JOBIM 2026"
date = 2026-06-03
description = "Visualization-driven pipeline for drug-design through generative AI"
theme="./static/style.css"
code_theme="lightfair"
+++

# Presentation available online

{{< qr text="https://filouplains.github.io/hugo_presentation/presentation/jobim_2026/" scale=10 />}}

**<https://filouplains.github.io/hugo_presentation/presentation/jobim_2026/>**

===

# Drug-design: cost and time-consuming

<br>

Review by Steven M. PAUL _et al._ in 2010\* shows:

- 2.8 billion USD of investissement
- 14 years to make a drug

<br>

> \*Paul, S. _et al._ How to improve R&D productivity: the pharmaceutical
> industry's grand challenge. Nat Rev Drug Discov 9, 203–214 (2010).
> <https://doi.org/10.1038/nrd3078>
{.small_note}

===

# AI is the solution?

<img src="./img/pubmed.png" height="650cm">

===

# Interpretability problem…

<br>

<div class="black-box">

black box

</div>

---

{{< grid template="1fr 1fr 1fr 1fr" >}}
<img src="./img/logo_ibpc.png" height="150cm">
<split>
<img src="./img/logo_lbt.png" height="150cm">
<split>
<img src="./img/logo_upcite.png" height="150cm">
<split>
<img src="./img/logo_cnrs.png" height="150cm">
{{< /grid >}}

<br>

# Visualization-driven pipeline for drug-design through generative AI

**Lucas ROUAUD**\
3^rd^ year PhD student

<br>

{{< grid template="1fr 1fr" >}}

<div align="left" class="title-page-footer">

**Director:** Marc BAADEN\
**Codirector:** Antoine TALY

</div>

<split>

<div align="right" class="title-page-footer">

IBPC - LBT - UMR 8266 UPC/CNRS\
ED 388

</div>

{{< /grid >}}

---

# Main pipeline objectives

<br>

1. Find a new ligand from an existing one
2. Have visualization method to understand what is happening

===

{{< svg src="./img/pipeline.svg" class="pipeline" >}}

---

{{< svg src="./img/pipeline.svg" id="input-step" class="pipeline" >}}

===

# `smiffer`

<br>

- Take in input a protein or an RNA
- Compute statistical interaction fields
- Physics based
- Hydrophobic, hydrophilic, H bond donor and acceptor, pi stacking, APBS

> Statistical Molecular Interaction Fields: A Fast and Informative Tool for Characterizing RNA and Protein-Binding Pockets.
> Diego Barquero Morera, Giovanni Mattiotti, Alexandar Kocev, Amshuman Rousselot, Louis Meuret, **Lucas Rouaud**, Hubert Santuz, Marc Baaden, Antoine Taly, and Samuela Pasquali.
> Journal of Chemical Theory and Computation 2025 21 (18), 9120-9135.
> DOI: 10.1021/acs.jctc.5c00688
{.small_note}

===

# `smiffer`

<br>

{{< grid template="1fr 1fr 1fr">}}

### Installation

{{< code language="bash" line_number=false >}}
$ pipx install \
    smiffer
{{< /code >}}
<split>

### Documentation

<https://smiffer.mol3d.tech/>
<split>

### Source code

<https://gitlab.galaxy.ibpc.fr/rouaud/smiffer>
<split>

{{< qr text="https://pypi.org/project/smiffer/" scale=7 />}}
<split>

{{< qr text="https://smiffer.mol3d.tech/" scale=7 />}}
<split>

{{< qr text="https://gitlab.galaxy.ibpc.fr/rouaud/smiffer" scale=7 />}}
<split>
{{< /grid >}}

===

# `strange`

- Take in input 1 or 2 molecules
- Compute pharmacophore in interaction (intra or between two elements)
- Works with MDAnalysis selection
- Output pharmacophore in interaction in `.csv`
- Output a visualization file

===

# `strange`

<br>

<div style="width: 80%; margin: auto;">

- Based on **pharmacophore**:
    > Set of sterics and electronics properties of a molecule to ensure optimal supramolecular interactions to trigger or block a biological response of a given target
- Why?
    - Generic, so the software works on any systems
    - Used by the AI to make ligands with the same properties

</div>

===

# `strange`

<br>

{{< grid template="1fr 1fr 1fr">}}

### Installation

{{< code language="bash" line_number=false >}}
$ pipx install \
    strange-mol
{{< /code >}}
<split>

### Documentation

<https://strange.mol3d.tech>
<split>

### Source code

<https://gitlab.galaxy.ibpc.fr/rouaud/strange>
<split>

{{< qr text="https://pypi.org/project/strange/" scale=7 />}}
<split>

{{< qr text="https://strange.mol3d.tech" scale=7 />}}
<split>

{{< qr text="https://gitlab.galaxy.ibpc.fr/rouaud/strange" scale=7 />}}
<split>
{{< /grid >}}

===

# Celecoxib in COX-2 (3LN1)

{{< molstar molxUrl="./static/visualization/celecoxib.molx" >}}

---

{{< svg src="./img/pipeline.svg" id="ai-step" class="pipeline" >}}

===

# Implemented scoring function

{{< 
    iframe src="./static/plot/scoring_function.html"
    width="1550px"
    height="750px"
>}}

===

# Scoring values (gaussian score)

{{< 
    iframe src="./static/plot/synthemol_result.html"
    width="1550px"
    height="750px"
>}}

===

# `SyntheMol`

<br>

{{< grid template="33% 1fr 1fr">}}

### Installation

{{< code language="bash" line_number=false >}}
$ pipx install \
        git+http://gitlab.galaxy.ibpc.fr/prabakaran/synthemol
{{< /code >}}
<split>

### Original source code

<https://github.com/swansonk14/SyntheMol>
<split>

### Source code

<https://gitlab.galaxy.ibpc.fr/prabakaran/synthemol>
<split>

{{< qr text="https://pypi.org/project/strange/" scale=7 />}}
<split>

{{< qr text="https://github.com/swansonk14/SyntheMol" scale=7 />}}
<split>

{{< qr text="https://gitlab.galaxy.ibpc.fr/prabakaran/synthemol" scale=7 />}}
<split>
{{< /grid >}}

---

{{< svg src="./img/pipeline.svg" id="preparation-step" class="pipeline" >}}

---

{{< svg src="./img/pipeline.svg" id="docking-step" class="pipeline" >}}

===

# Uni-Dock

<br>

{{< grid template="2fr 1fr" >}}

- GPU accelerated
- Can use SDF (do not work) or PDBQT for the ligand
- Can use PDB or PDBQT for the protein
- Can use Vinardo scoring function
- Open source: <https://github.com/dptech-corp/Uni-Dock>

<split>

{{< qr text="https://github.com/dptech-corp/Uni-Dock/" scale=7 />}}

{{< /grid >}}

===

# Scoring repartition

{{< 
    iframe src="./static/plot/docking_score.html"
    width="1550px"
    height="750px"
>}}

---

{{< svg src="./img/pipeline.svg" id="output-step" class="pipeline" >}}

===

# _I'll be the very best!_

{{< molstar molxUrl="./static/visualization/mol_195_out.molx" >}}

---

# Conclusion

- The whole pipeline works
- Rework the matching algorithm
- Test the scoring function (inverse vs Gaussian)
- Need to apply the whole pipeline to other system
- Write my PhD manuscript…

___

# Thanks for your attention!

<div class="lab_member">
    <img src="./img/lbt.jpeg" width="80%">
    <img src="./img/project_member/marc_baaden.jpg" width="200cm">
    <img src="./img/project_member/malek_melliti.jpg" width="200cm">
    <img src="./img/project_member/antoine_taly.jpg" width="200cm">
    <img src="./img/project_member/isleme_khalfaoui.jpeg" width="200cm">
    <img src="./img/project_member/etienne_reboul.jpg" width="200cm">
</div>
