+++
title = "Soutenance de thèse"
date = 2026-10-23
description = "Combinaison de méthodes de visualisation à de l'IA générative dans le cadre du drug design"
theme="./static/style.css"
code_theme="lightfair"
+++

# Je ne sais qu'une chose, <br> c'est que je ne sais rien

**— Socrate**

---

# Conception de médicaments

<br>

- Un enjeu sanitaire et économique important ;

- requiert des investissements de long terme et financièrement lourd :

    - une durée pouvant aller jusqu'à 14 ans ;

    - des revues relèvent des investissements financiers allant de 314 millions USD à 2,8 millards USD.

===

# Aucune garantie de succès

<img src="./img/step_drug_development.png" width="80%">

**© Steven M. PAUL et collaborateur, 2010, _modifiée_**

===

# Contrer cela : développement de nouvelles méthodes

- Développement de nouvelles méthodes informatiques, comme l'amarrage moléculaire ;

- augmentation des tailles des bases de données (comme la PDB avec des structures protéiques) ;

- amélioration des systèmes informatiques.

===

# Apparition de l'intelligence artificielle (IA) générative

<br>

- Concepte datant de 1913 avec les chaînes de Markov :

    - probabilités d'enchaînement des lettres ne sont pas indépendantes ;

    - il est possible de générer une matrice d'enchaînement de ces lettres ;

    - à partir de cette matrice, la génération de texte devient possible.

> **Objectif global d'une IA générative identique**
>
> Déterminer une distribution soujacente à des objets donnés (texte, image, etc.) pour pouvoir en générer d'autres.

===

# Plusieurs modèle, un cœur commun

- Il y a plusieurs modèles d'IA générative _(modèle de diffusion, auto-encodeur varioationnel, réseaux antagonistes génératifs, transformeurs génératifs préentraînés)_ ;
- tous basés sur les neurones artificiels, l'origine de la qualification de ces modèles de « boîte noire ».

<br>
<br>

<img src="./img/artificial_neural_network.svg" width="40%">

===

# Apparition de l'IA explicable

- Faire en sorte de pouvoir comprendre et interpréter l'origine des résultats obtenus ;

- différentes méthodes :
    
    - explicabilité des données ;

    - explicabilité par le modèle ;

    - analyses _post hoc_ ;

    - utilisation de moyens de visualisations.

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

## Temps d'exécution

<img src="./img/smiffer_execution_time.svg" width="80%">

===

## Résultat

{{<
    molstar
    molxUrl="./static/smiffer_diazépam.molx"
>}}

---

# Calcul des interactions directes

===

## Temps d'exécution

<img src="./img/strange_execution_time.svg" width="100%">

===

## Comparaison des interactions détectées

<img src="./img/strange_detected_interaction.svg" width="39%">

===

## Résultat

{{<
    molstar
    molxUrl="./static/strange_diazépam.molx"
>}}

---

# Génération de nouveaux ligands

===

## Fonction de score

<br>

$$
\begin{aligned}
    pénalité &= recherché - correspond + max(0, généré - recherché) \\[1em]
    inverse(pénalité) &= \dfrac{1}{1 + pénalité} \\[1em]
    gaussienne(pénalité) &= \exp \left( - \dfrac{\left( pénalité \right)^2}{2 \cdot \sigma^2} \right) \\[1em]
\end{aligned}
$$

===

{{<
    iframe src="./static/scoring_function.html"
    width="1550px"
    height="750px"
>}}

===

## Base de données de blocs

<img src="./img/molecular_descriptor.svg" width="40%">

===

## Projection des blocs et des molécules

<img src="./img/tsne.svg" width="40%">

===

## Score par rapport à la génération des ligands

<img src="./img/pharmacophore_score.svg" width="80%">

===

## Meilleures molécules générées

<br>

{{< grid template="1fr 1fr 1fr" >}}
<img src="./img/best_molecule_3.svg" width="80%" style="border: red 5pt solid;">
<split>
<img src="./img/best_molecule_2.svg" width="80%">
<split>
<img src="./img/best_molecule_1.svg" width="80%">
<split>
{{< /grid >}}

---

# Convertion des ligands au format adéquat

<br>

- filtrage « des atomes-ancres » (B, Hg, Mg, Np, Sn, U) ;
- filtrage des distance interatomiques anormales (0,7 à 3 Å) ;
- conversion au format `.pdbqt` via `meeko`.

===

## Résultat

{{<
    molstar
    molxUrl="./static/ligand_conversion.molx"
>}}

---

# Amarrage moléculaire des nouveaux ligands

===

## Distribution des scores

<img src="./img/docking_score_result.svg" width="40%">

===

## Erreur de conversion au format `.pdbqt` du diazépam

{{<
    molstar
    molxUrl="./static/diazepam_bug.molx"
>}}

===

## Score d'amarrage par rapport au score pharmacophore

<img src="./img/synthemol_vs_unidock.svg" width="40%">

===

## Interaction détectée après l'amarrage : `SyntheMol`

{{<
    molstar
    molxUrl="./static/best_synthemol.molx"
>}}

===

## Interaction détectée après l'amarrage : `Uni-Dock`

{{<
    molstar
    molxUrl="./static/best_unidock.molx"
>}}

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
