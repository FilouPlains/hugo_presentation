+++
title = "Soutenance de thèse"
date = 2026-10-23
description = "Combinaison de méthodes de visualisation à de l'IA générative dans le cadre du drug design"
theme="./static/style.css"
code_theme="lightfair"
+++

<h1 style="font-size: 3em;">Je ne sais qu'une chose, <br> c'est que je ne sais rien</h1>

**— Socrate**

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

# Combinaison de méthodes de visualisation à de l’intelligence artificielle générative dans le cadre de conception de médicament
 

**Lucas ROUAUD**\
23 octobre 2026

<br>

{{< grid template="1fr 1fr" >}}

<div align="left" class="title-page-footer">

**Directeur:** Marc BAADEN\
**Codirecteur:** Antoine TALY

</div>

<split>

<div align="right" class="title-page-footer">

IBPC - LBT - UMR 8266 UPC/CNRS\
ED 388

</div>

{{< /grid >}}

---

# Présentation du système

<img src="./img/neurone.svg" width="40%">

===

## Structure

{{<
    molstar
    molxUrl="./static/6x3x.molx"
>}}

---

# Préparation du système

<br>

- Utilisation de deux scripts `Python` :
    - `extract_clean_protein.py` :
        1. extrait seulement la protéine d'intérêt ;
        2. lance `Modeller` pour combler les trous de la protéines (modèle « tout hydrogènes ») ;

    - `relax_system.py` :
        minimise le système pour le relaxer via `OpenMM`.

- RMSD entre les carbonnes alpha support (`6x3x`) et le système final de **0,2 Å**.

===

## Résultat

{{<
    molstar
    molxUrl="./static/pdb_vs_prepared.molx"
>}}

---

# Calcul des champs d'interaction

===

## Résultat

{{<
    molstar
    molxUrl="./static/smiffer_diazépam.molx"
>}}

---

# Calcul des interactions directes

===

## Résultat

{{<
    molstar
    molxUrl="./static/strange_diazépam.molx"
>}}

---

# Génération de nouveaux ligands

===

# Fonction de score

$$
score(x) = \dfrac{1}{1 + recherché - correspond + max(0, généré - recherché)}
$$

## Inverse

$$
score(x) = \dfrac{1}{1 + pénalité}
$$


## Gaussienne

$$
score(x) = \exp \left( - \dfrac{\left( research - correspond + max(0, generate - research) \right)^2}{2 \cdot \sigma^2} \right)
$$

$$
score(x) = \exp \left( - \dfrac{\left( research - correspond + max(0, generate - research) \right)^2}{2 \cdot \sigma^2} \right)
$$

===

{{<
    iframe src="./static/scoring_function.html"
    width="1550px"
    height="750px"
>}}

---

# Convertion des ligands au format adéquat

---

# Amarrage moléculaire des nouveaux ligands

---

# Analyse des poses obtenues

---

# Merci de votre attention

<div class="lab_member">
    <img src="./img/lbt.jpeg" width="80%">
    <img src="./img/project_member/marc_baaden.jpg" width="200cm">
    <img src="./img/project_member/malek_melliti.jpg" width="200cm">
    <img src="./img/project_member/antoine_taly.jpg" width="200cm">
    <img src="./img/project_member/isleme_khalfaoui.jpeg" width="200cm">
    <img src="./img/project_member/etienne_reboul.jpg" width="200cm">
</div>
