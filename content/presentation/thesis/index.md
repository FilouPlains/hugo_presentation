+++
title = "Soutenance de thèse"
date = 2026-10-23
description = "Combinaison de méthodes de visualisation à de l'IA générative dans le cadre du drug design"
theme="./static/style.css"
code_theme="lightfair"
+++

<!-- .slide: data-background="#000" -->

## Je ne sais qu'une chose, <br> c'est que je ne sais rien

**— Socrate**

---

# Conception de médicaments

<br>

- Un enjeu sanitaire et économique important ;

- requiert des investissements de long terme et financièrement lourd :

    - une durée pouvant aller jusqu'à 14 ans ;

    - des revues relèvent des investissements financiers allant de 314 millions USD à 2,8 millards USD.

===

### Aucune garantie de succès

<img src="./img/step_drug_development.png" width="80%">

**© Steven M. PAUL et collaborateur, 2010, _modifiée_**

===

### Contrer cela : développement de nouvelles méthodes

- Développement de nouvelles méthodes informatiques, comme l'amarrage moléculaire ;

- augmentation des tailles des bases de données (comme la PDB avec des structures protéiques) ;

- amélioration des systèmes informatiques.

===

### Apparition de l'intelligence artificielle (IA) générative

<br>

- Concepte datant de 1913 avec les chaînes de Markov :

    - probabilités d'enchaînement des lettres ne sont pas indépendantes ;

    - il est possible de générer une matrice d'enchaînement de ces lettres ;

    - à partir de cette matrice, la génération de texte devient possible.

> **Objectif global d'une IA générative identique**
>
> Déterminer une distribution soujacente à des objets donnés (texte, image, etc.) pour pouvoir en générer d'autres.

===

### Plusieurs modèle, un cœur commun

- Il y a plusieurs modèles d'IA générative _(modèle de diffusion, auto-encodeur varioationnel, réseaux antagonistes génératifs, transformeurs génératifs préentraînés)_ ;
- tous basés sur les neurones artificiels, l'origine de la qualification de ces modèles de « boîte noire ».

<br>
<br>

<img src="./img/artificial_neural_network.svg" width="40%">

===

### Apparition de l'IA explicable

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

## Combinaison de méthodes de visualisation à de l’intelligence artificielle générative dans le cadre de conception de médicament
 

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

## Objectifs

- Avoir une IA qui génère des ligands et dont l'origine des résultats sont compréhensibles :

    - « l'humain » doit pouvoir lancer les calculs et comprendre chaque étape ;

    - permet de corriger des problèmes ou d'améliorer le programme ;

- basé sur des propriétés déjà connues ou imposées :

    - optimisation de ligands ;

    - retrouver des analogues à un ligand donné.

===

<img src="./img/pipeline.svg" width="40%">

===

## Présentation du système

{{< grid template="1fr 1fr" >}}

- Récepteur à l'acide gamma-amino butyrique de type A (récepteur GABA A) ;

- système complexe bien connue : canal ionique hétéropentamère, transmembranaire et allostérique ;

- constitué de trois types de sous-unités, ayant plusieurs variants ($\alpha$ 1-6, $\beta$ 1-3, $\gamma$ 1-3, $\delta$, $\pi$ et $\theta$) ;

- fixation de GABA provoque l'influx d'ions chlorures, empêchant la création d'un potentiel d'action, bloquant la transduction d'un signal nerveux.

<split>

<img src="./img/neurone.svg" width="80%">
{{< /grid >}}

===

### Étude du complexe récepteur GABA A avec le diazépam

- Étude du diazépam, un benzodiazépine :

    - rôle relaxant et anticonvulsant ;

    - possède différents effets secondaires, comme la dépendance physique.

> **Objectif**
>
> Retrouver un analogue du diazépam, soit une molécule ayant des propriétés physico-chimiques semblables.

===

### Structure

{{<
    molstar
    molxUrl="./static/6x3x.molx"
>}}

---

<img src="./img/pipeline.svg" width="40%">

===

## Préparation du système

<br>

- Important pour plusieurs raisons :

    - l'amarrage moléculaire est dépendant du système de départ ;

    - pour les calculs des interactions (champs et directes), besoin d'avoir les hydrogènes et une structure complète ;

    - besoin de relaxer le système pour que `strange` puisse fonctionner correctement à partir d'un fichier `.pdb`.

===

### Méthode

<br>

- Utilisation de deux scripts `Python` :
    - `extract_clean_protein.py` :
        1. extrait seulement la protéine d'intérêt ;
        2. lance `Modeller` pour combler les trous de la protéines (modèle « tout hydrogènes ») ;

    - `relax_system.py` :
        minimise le système pour le relaxer via `OpenMM`.

- RMSD entre les carbonnes alpha support (`6x3x`) et le système final de **0,2 Å**.

===

### Résultat

{{<
    molstar
    molxUrl="./static/pdb_vs_prepared.molx"
>}}

---

<img src="./img/pipeline.svg" width="40%">

===

## Calcul des champs d'interaction

{{< grid template="1fr 1fr" >}}

- **Utilisation de `smiffer` :**

    - logiciel codéveloppé ;

    - fonctionne sur une protéine ou un ARN ;

    - calcul des champs d'interactions statistiques ;

    - basé sur la physique ;

    - somme de gaussienne

<split>

<img src="./img/smiffer_fields.png" width="100%">
{{< /grid >}}

> Statistical Molecular Interaction Fields: A Fast and Informative Tool for Characterizing RNA and Protein-Binding Pockets.
> Diego Barquero Morera, Giovanni Mattiotti, Alexandar Kocev, Amshuman Rousselot, Louis Meuret, **Lucas Rouaud**, Hubert Santuz, Marc Baaden, Antoine Taly, and Samuela Pasquali.
> Journal of Chemical Theory and Computation 2025 21 (18), 9120-9135.
> DOI: 10.1021/acs.jctc.5c00688
{.small_note}

===

### Étapes pour filtrer les grilles

<img src="./img/smiffer_filtrage.png" width="60%">

===

### Résultat

{{<
    molstar
    molxUrl="./static/smiffer_diazépam.molx"
>}}

---

<img src="./img/pipeline.svg" width="40%">

===

## Calcul des interactions directes

- **Utilisation de `strange` :**

    - logiciel développé ;

    - permet de calculer des pharmacophores en interactions :
        - _ensemble de propriétés stériques / électroniques garantissant des interactions supramoléculaires, provoquant une réponse d'une cible biologique_ ;
        - utilisation de critères géométriques ;
        - prend en compte les ponts salins, les interactions hydrophobes, les liaisons hydrogènes et halogènes, les empilements $\pi$, les interactions $\pi$ cation / anion ;

    - permet d'être générique, donc indépendant du système donnée en entrée (ARN, protéine, sucre, ligand, etc.) ;

    - les pharmacophores extraient peuvent être utilisés pour l'étape de génération des ligands.

===

### Résultat

{{<
    molstar
    molxUrl="./static/strange_diazépam.molx"
>}}

===

### Pharmacophores du diazépam

| Pharmacophores            |   Sous-famille   |  ID  |
| :------------------------ | :--------------: | :--: |
| **Accepteur d'halogène**  | Accepteur simple |  O2  |
| **Donneur d'halogène**    |  Donneur simple  | Cl0  |
| **Hydrophobe**            |     Regroupé     |      |
| **Hydrophobe**            |     Regroupé     |      |
| **Aromatique**            |    Cycle de 6    |      |
| **Aromatique**            |    Cycle de 6    |      |
| **Positif**               |  Groupe basique  | N16  |
| **Accepteur d'hydrogène** | Accepteur simple |  O2  |
| **Donneur d'hydrogène**   |  Donneur simple  | N16  |

---

<img src="./img/pipeline.svg" width="40%">

===

## Génération de nouveaux ligands

===

### Recherche Arborescente Monte-Carlo

{{< grid template="1fr 1fr" >}}
<img src="./img/synthemol_bloc.svg" width="100%">
<split>
<img src="./img/synthemol_mcts.svg" width="75%">
{{< /grid >}}

===

### Détection de points de pharmacophores communs

{{< grid template="1fr 1fr" >}}
<img src="./img/synthemol_match.svg" width="80%">

<split>

<img src="./img/synthemol_graphe.svg" width="80%">
{{< /grid >}}

===

### Fonction de score

<br>

> Une valeur de $0$ indique un score mauvais, une valeur de $1$ une valeur de score optimale.

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

### Base de données de blocs

<img src="./img/molecular_descriptor.svg" width="40%">

===

### Projection des blocs et des molécules

<img src="./img/tsne.svg" width="40%">

===

### Score par rapport à la génération des ligands

<img src="./img/pharmacophore_score.svg" width="80%">

===

### Meilleures molécules générées ($score = 0,73$)

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

<img src="./img/pipeline.svg" width="40%">

===

## Convertion des ligands au format adéquat

---

<img src="./img/pipeline.svg" width="40%">

===

## Amarrage moléculaire des nouveaux ligands

<br>

- Permet de vérifié l'affinité d'un ligand avec une cible ;

- utilisation d'`Uni-Dock` avec la fonction de score `Vinardo` :
    
    - `Vinardo` permet de ne pas avoir de corrélation « taille du ligand » / « affinité » ;

    - Permet d'amarrer rapidement les molécules via un GPU.

===

### Distribution des scores

<img src="./img/docking_score_result.svg" width="40%">

===

### Erreur de conversion au format `.pdbqt` du diazépam

{{<
    molstar
    molxUrl="./static/diazepam_bug.molx"
>}}

===

### Score d'amarrage par rapport au score pharmacophore

<img src="./img/synthemol_vs_unidock.svg" width="40%">

===

### Interaction détectée après l'amarrage : `SyntheMol`

{{<
    molstar
    molxUrl="./static/best_synthemol.molx"
>}}

===

### Interaction détectée après l'amarrage : `Uni-Dock`

{{<
    molstar
    molxUrl="./static/best_unidock.molx"
>}}

===

### Comparaison avec le diazépam

| Catégorie                        | Diazépam                   | Meilleur ligand `SyntheMol` | Meilleur ligand `Uni-Dock` |
| -------------------------------- | -------------------------- | --------------------------- | -------------------------- |
| **Score pharmacophores**         | 1.0                        | 0.73                        | 0.20                       |
| **Score d'amarrage moléculaire** | 3.202 kcal/mol             | -7.630 kcal/mol             | -9.587 kcal/mol            |
| **-**                            | **Intéractions détectées** |                             |                            |
| **Liaison halogène**             | HIS.093.D                  | -                           | -                          |
| **Liaison halogène**             | -                          | SER.150.D                   | -                          |
| **Hydrophobe**                   | TYR.201.D                  | -                           | -                          |
| **Hydrophobe**                   | TYR.151.D                  | -                           | -                          |
| **Hydrophobe**                   | _PHE.091.D_                | _PHE.091.D_                 | -                          |
| **Hydrophobe**                   | -                          | VAL.194.D                   | -                          |
| **Empilement $\pi$**             | _TYR.201.D_                | -                           | _TYR.201.D_                |
| **Empilement $\pi$**             | -                          | TYR.034.E                   | TYR.034.E                  |
| **Empilement $\pi$**             | -                          | -                           | PHE.053.E                  |
| **Cation $\pi$**                 | PHE.053.E                  | -                           | -                          |
| **Liaison hydrogène**            | SER.197.D                  | -                           | -                          |

---

## Conclusion

<br>

- `smiffer` codéveloppé pour visualiser des champs d'interaction ;

- `strange` développé pour visualiser des interactions directes ;

- développement de « logiciels ponts » et agencement de différent logiciel pour avoir une chaîne de traitement qui marche ;

- les moyens de visualisations permettent de comprendre certains résultats ;

- application sur un système concret, le récepteur GABA A, correcte.

===

## Tests en cours

- Variation au niveau des paramètres de `SyntheMol` ;

- tests de la chaîne de traitement avec des ARN ;

- analyses comparatives (_benchmark_) par rapport à différentes cibles.

===

## Perpectives

<br>

- **Calcul des champs d'interactions :**
    - utilisation de pharmacophore pour inférer les champs ;
    - inférer des pharmacophores d'un ligand à partir des champs ;

- **calcul des interactions directes :**
    - amélioration des performances ;
    - rajout et correction du calcul de certaines interactions ;

- **génération des ligands :**
    - amélioration des performances : 12 heures, 55 GB de mémoire ;
    - amélioration de la fonction de score ;
    - problème de surreprésentation de certains points pharmacophoriques.

===

## Perpectives

<br>

- **Conversion en 3D des ligands :**
    - problème pouvant affecter la détection d'un potentiel bon ligand ;

- **amarrage moléculaire :**
    - amarrage avec des résidus flexibles ;
    - correction de la zone d'amarrage ;

- **pipeline au global :**
    - utilisation de `Snakemake` (répétabilité et modularité) ;
    - ajout de métadonnées ;
    - correction de certains filtre (20 % des meilleurs ligands).

---

## Merci de votre attention

<div class="lab_member">
    <img src="./img/lbt.jpeg" width="80%">
    <img src="./img/project_member/marc_baaden.jpg" width="200cm">
    <img src="./img/project_member/malek_melliti.jpg" width="200cm">
    <img src="./img/project_member/antoine_taly.jpg" width="200cm">
    <img src="./img/project_member/isleme_khalfaoui.jpeg" width="200cm">
    <img src="./img/project_member/etienne_reboul.jpg" width="200cm">
</div>

---

<!-- .slide: data-visibility="uncounted" -->

## Annexes

---

<!-- .slide: data-visibility="uncounted" -->

## smiffer

===

### Équations pour calculer les champs

$$
\begin{align}
\phi_{\text{liaison H}} &= - \sum_{\text{atome } i = 1}^{\text{atomes select.}} \exp\left( - \frac{(\mu_d - d_{\text{atome } i})^2}{2 \cdot \sigma^2_d} \right) \times \exp\left( - \frac{(\mu_\beta - \beta_{\text{atome } i})^2}{2 \cdot \sigma^2_\beta} \right) \\[1em]
\phi_{\text{hydroph.}} &= - \sum_{\text{espèce } i = 1}^{\text{espèces select.}} K_{\text{espèce}} \times \sum_{\text{atome } i = 1}^{\substack{\text{atomes} \\ \text{espèces select.}}} \exp\left( - \frac{(\mu_{\text{hydroph.}} - d_{\text{espèce}})^2}{2 \cdot \sigma^2_{\text{hydroph.}}} \right) \\[1em]
\phi_{\pi} &= - \sum_{\text{cycle } i = 1}^{\text{cycles select.}} \exp\left( - \frac{(\mathbf{v}_r - \mathbf{\mu}_{\pi})^\top \cdot \mathbf{S}_{\pi}^{-1} \cdot \mathbf{v}_r - \mathbf{\mu}_{\pi}}{2} \right) \\[1em]
\end{align}
$$

---

<!-- .slide: data-visibility="uncounted" -->

## strange

===

<!-- .slide: data-visibility="uncounted" -->

### Définition d'un pharmacophore

{{< grid template="1fr 1fr" >}}

Un pharmacophore désigne un ensemble de caractéristiques stériques et électroniques.
Cet ensemble est nécessaire pour garantir des interactions supramoléculaires optimales avec une structure cible biologique spécifique.
Ces interactions permettent de déclencher ou de bloquer la réponse biologique de la dite cible.

— D'après _IUPAC Recommendations 1998_

<split>

<img src="./img/strange_pharmacophore.svg" width="60%">
{{< /grid >}}

===

<!-- .slide: data-visibility="uncounted" -->

### Utilisation de critères géométriques pour détecter les différentes interactions

<img src="./img/strange_interaction_constante.svg" width="80%">


---

<!-- .slide: data-visibility="uncounted" -->

## SyntheMol

===

<!-- .slide: data-visibility="uncounted" -->

{{< grid template="1fr 1fr" >}}
### _Simplified Molecular Input Line Entry System_ (SMILES)

<split>

<img src="./img/synthemol_smiles.svg" width="80%">

{{< /grid >}}

===

<!-- .slide: data-visibility="uncounted" -->

### _SMiles ARbitrary Target Specification_ (SMARTS)

<br>

`[C;D1]-N=C-[N,S]`

<br>

<img src="./img/synthemol_smarts.svg" width="80%">

===

<!-- .slide: data-visibility="uncounted" -->

### SMIRKS

<br>

{{< grid template="1fr 1fr" >}}
<img src="./img/synthemol_regex.png" width="100%">

<split>

<img src="./img/synthemol_smirks.svg" width="100%">
{{< /grid >}}

---

<!-- .slide: data-visibility="uncounted" -->

## Convertion en `.pdbqt`

===

<!-- .slide: data-visibility="uncounted" -->

# Étapes pour la conversion

<br>

- **Passage du format « SMILES » 1D à un format 3D :**

    - **utilisation de `Gypsum-DL` :**

        - ionisation des ligands ;

        - génération des différentes conformations ;

        - minimisation ;

    - **conversion au format `.pdbqt` via `meeko` :**

        - filtrage « des atomes-ancres » (B, Hg, Mg, Np, Sn, U) ;

        - filtrage des distance interatomiques anormales (0,7 à 3 Å).

===

<!-- .slide: data-visibility="uncounted" -->

### Résultat

{{<
    molstar
    molxUrl="./static/ligand_conversion.molx"
>}}
