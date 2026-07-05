# GVH Dynamic 0.1 — Volume de synthèse

**Auteur :** Charlemagne O. Laurince
**Version :** 0.1
**Statut :** descriptif, méthodologique et reproductible — indépendant de toute interprétation physique liée au Volume Partagé (VP)

---

## 1. Introduction

Ce volume rassemble et compare les résultats obtenus dans l'ensemble des pipelines **GVH Dynamic 0.1** appliqués à huit systèmes de nature très différente : trois systèmes dynamiques chaotiques (Lorenz, Rössler, Duffing), un benchmark de calibration à référence analytique connue (Gravity Train), et quatre jeux de données cosmologiques (Pantheon+, H(z), BAO, CMB).

L'objectif de GVH Dynamic est de vérifier qu'**un même cadre géométrique général** — construit uniquement à partir de la structure discrète d'une trajectoire ou d'une série de points $X_i \in \mathbb{R}^d$ — permet de produire des observables comparables, quelle que soit la nature physique du système étudié, avec certaines conventions opératoires encore spécifiques aux jeux de données dans cette version 0.1 (voir §2.3).

Cette version 0.1 est volontairement limitée à la définition, au calcul et à la comparaison des observables géométriques. **Aucune interprétation physique fondamentale n'est proposée ici** ; une éventuelle interprétation relèvera d'un cadre théorique distinct (VP–GVH), traité séparément.

---

## 2. Cadre méthodologique commun

Tous les pipelines reposent sur un objet géométrique unique : une suite de points $X_i \in \mathbb{R}^d,\ i=1,\ldots,N$, représentant selon le cas une trajectoire dynamique, une série cosmologique ou une carte de température.

### 2.1 Les dix observables GVH

| Symbole | Nom | Définition |
|---|---|---|
| $D_T(i)$ | Variation locale | $\|\Delta X_i\| = \|X_{i+1}-X_i\|$ |
| $D_T^{\rm mean}$ | Variation locale moyenne | $\overline{D_T}$ |
| $S_T$ | Dispersion | $\sigma(D_T)$ |
| $S_T^{\rm norm}$ | Dispersion normalisée | $S_T / \overline{D_T}$ |
| $D_c$ | Seuil critique | quantile (généralement $Q_{0.90}$, ou $\overline{D_T}+S_T$, ou $\overline{D_T}+2S_T$ selon le pipeline) |
| $R_{\rm super}$ | Fraction supercritique | fraction des $D_T(i) > D_c$ |
| $A_H,\ B_H$ | Loi hiérarchique | ajustement $R_{\rm super}(D_c) \approx A_H e^{-B_H D_c}$ |
| $\theta_{\rm mean}$ | Angle moyen | angle moyen entre incréments successifs |
| $\theta_{\max}$ | Angle maximal | angle maximal observé |
| $R_{180}$ | Quasi-opposition | fraction des angles $> 170°$ |

### 2.2 Principe de comparabilité

Ces définitions sont **indépendantes de la nature physique des données** : la même chaîne de calcul (variation locale → dispersion → seuil → loi hiérarchique → angles) s'applique identiquement à une trajectoire dans l'espace des phases, à une série $(z, H(z))$, ou à une carte de température 2D.

### 2.3 Écarts méthodologiques observés entre pipelines (0.1)

La comparaison directe des huit pipelines révèle que la version 0.1 n'est pas parfaitement homogène sur certains points, à corriger dans les versions futures :

- **Définition de $D_c$** : $Q_{0.90}(D_T)$ dans les définitions communes et pour Lorenz/Rössler/Duffing/Gravity Train ; $\overline{D_T}+2\sigma(D_T)$ pour Pantheon+ et CMB ; $\overline{D_T}+\sigma(D_T)$ dans une variante de Lorenz.
- **Définition de $A_H,\ B_H$** : ajustement exponentiel de $R_{\rm super}(D_c)$ pour les systèmes chaotiques, Gravity Train, CMB et Pantheon+ ; formule directe $A_H=\max(D_T)-\min(D_T)$, $B_H=A_H/\overline{D_T}$ pour BAO.
- **Observables angulaires non calculées** pour BAO (séries trop courtes).

Ces variations n'invalident pas les résultats mais imposent une **prudence de lecture** lors des comparaisons inter-pipelines strictes ; elles constituent une piste de standardisation pour GVH Dynamic 0.2.

---

## 3. Partie I — Systèmes dynamiques chaotiques

### 3.1 Protocole commun

Les trois systèmes (Lorenz, Rössler, Duffing) sont intégrés numériquement (`solve_ivp`, méthode RK45, tolérances $10^{-9}/10^{-12}$), avec suppression des 20 % premiers points (régime transitoire) pour Lorenz et Rössler. Le signal GVH est construit soit directement sur l'état $(x,y,z)$ (Lorenz, Rössler), soit sur $T(t)=\sqrt{x(t)^2+v(t)^2}$ (Duffing).

| Paramètre | Lorenz | Rössler | Duffing |
|---|---|---|---|
| Équations | $\dot x=\sigma(y-x)$, $\dot y=x(\rho-z)-y$, $\dot z=xy-\beta z$ | $\dot x=-y-z$, $\dot y=x+ay$, $\dot z=b+z(x-c)$ | $\ddot x+\delta\dot x+\alpha x+\beta x^3=\gamma\cos(\omega t)$ |
| Paramètres | $\sigma=10,\ \rho=28,\ \beta=8/3$ | $a=0.2,\ b=0.2,\ c=5.7$ | $\delta=0.2,\ \alpha=-1,\ \beta=1,\ \gamma=0.3,\ \omega=1.2$ |
| $t$, $N$ | $[0,250]$, 50 000 | $[0,500]$, 50 000 | $[0,500]$, 20 000 |
| Transitoire retiré | 20 % | 20 % | non applicable |

### 3.2 Tableau comparatif des observables

| Observable | Lorenz | Rössler | Duffing |
|---|---|---|---|
| $D_T^{\rm mean}$ | 0.469336 | 0.086982 | 0.293183 |
| $S_T$ | 0.284268 | 0.079914 | 0.203821 |
| $S_T^{\rm norm}$ | 0.605681 | 0.918746 | 0.695200 |
| $D_c$ | 0.753603 | 0.166896 | 0.665159 |
| $R_{\rm super}$ | 0.156629 | 0.064802 | 0.050000 |
| $A_H$ | 1.722010 | 2.157931 | 1.909376 |
| $B_H$ | 3.234647 | 22.474675 | 4.784771 |
| $\theta_{\rm mean}$ | 2.428216° | 0.721336° | 1.746517° |
| $\theta_{\max}$ | 6.143509° | 12.562516° | 17.910256° |
| $R_{180}$ | 0.000000 | 0.000000 | 0.000000 |

### 3.3 Discussion

Les trois systèmes chaotiques partagent une signature commune : des **angles faibles** ($\theta_{\rm mean} < 3°$) et une **absence totale d'opposition angulaire** ($R_{180}=0$), traduisant une continuité directionnelle locale des trajectoires malgré le chaos sous-jacent. En revanche, la dispersion multi-échelle ($S_T^{\rm norm}$) et la pente de décroissance hiérarchique ($B_H$) varient sensiblement d'un système à l'autre (facteur ~7 entre Rössler et Lorenz sur $B_H$), ce qui suggère que ces deux observables portent une information discriminante sur la nature de chaque attracteur, contrairement aux observables angulaires qui semblent plus universelles pour ce type de dynamique lisse.

Dans chaque pipeline, il est noté que $B_H$ reste sensible à la fenêtre d'ajustement choisie et doit donc être traité comme un paramètre descriptif de convention, non comme une constante physique.

---

## 4. Partie II — Benchmark de calibration : le Gravity Train

### 4.1 Objectif

Contrairement aux trois systèmes précédents, le *gravity train* possède une **solution analytique de référence connue** : dans une Terre homogène idéale ($\rho(r)=\rho_0$), tous les tunnels rectilignes traversant la Terre ont le même temps de traversée, quelle que soit leur profondeur — un résultat classique de mécanique. Ce pipeline teste si GVH Dynamic est capable de **détecter la rupture** de cette invariance harmonique lorsqu'on passe à une Terre radialement stratifiée (densité réaliste $\rho(r)$).

### 4.2 Modèles comparés

- **Modèle A (homogène)** : $\ddot{x}=-\omega^2 x$, dynamique harmonique exacte, indépendante du paramètre d'impact $b$.
- **Modèle B (stratifié)** : $\ddot{x} = -\dfrac{GM(\sqrt{x^2+b^2})}{(x^2+b^2)^{3/2}}\,x$, dynamique non harmonique dépendant de $b$.

Dix tunnels sont testés, $b = 0, 0.1R, \ldots, 0.9R$ ($R=R_{\rm Terre}$).

### 4.3 Résultats

| Observable | Modèle A (homogène) | Modèle B (stratifié) |
|---|---|---|
| $S_T^{\rm norm}$ | 0.2505 | 0.4729 |
| $D_c$ | 0.002096 | 0.003042 |
| $B_H$ | 3025.67 | 1343.73 |
| $\theta_{\rm mean}$ | 0.090026° | 0.114299° |
| $\theta_{\max}$ | 0.127343° | 31.560064° |
| $R_{180}$ | 0 | 0 |

### 4.4 Discussion

Le résultat central est sans ambiguïté : **GVH Dynamic détecte la rupture de l'invariance harmonique** induite par la stratification. L'élargissement de $S_T^{\rm norm}$, la diminution de $B_H$ et surtout l'explosion de $\theta_{\max}$ (0.13° → 31.6°) constituent une signature claire et cohérente du changement de régime dynamique entre les deux modèles.

Ce pipeline joue un rôle de **validation méthodologique** pour l'ensemble du volume : c'est le seul cas où la « bonne réponse » est connue à l'avance (invariance exacte en Modèle A), ce qui permet de calibrer la sensibilité du cadre GVH avant de l'appliquer à des systèmes purement empiriques ou chaotiques.

---

## 5. Partie III — Données cosmologiques

### 5.1 Vue d'ensemble

Quatre jeux de données cosmologiques sont traités : le catalogue de supernovae **Pantheon+**, les mesures directes du taux d'expansion **H(z)**, les oscillations acoustiques baryoniques **BAO** (SDSS DR12), et une carte **CMB** — synthétique dans cette version 0.1, en attente d'une vraie carte (Planck) pour une future itération.

### 5.2 Tableau comparatif

| Observable | Pantheon+ | H(z) | BAO ($D_M/r_s$) | BAO ($H(z)r_s$) | CMB (synthétique) |
|---|---|---|---|---|---|
| $D_T^{\rm mean}$ | 2876.48 | 13.708950 | 3432.075585 | 77.725846 | 0.894951 |
| $S_T$ | 0.1505* | 13.421900 | 100.562283 | 2.475762 | 0.474084 |
| $D_c$ | 12631.61 | 35.000000 | 3532.463813 | 80.092154 | 1.843118 |
| $R_{\rm super}$ | 0.06284 | 0.096774 | 0.333333 | 0.333333 | 0.035919 |
| $A_H$ | 22166.62 | 1.175518 | 245.630769 | 6.047231 | 1.417348 |
| $B_H$ | 0.000176 | 0.085848 | 0.071569 | 0.077802 | 2.212726 |
| $\theta_{\rm mean}$ | 73.22° | 116.479433° | — | — | 90.160201° |
| $\theta_{\max}$ | 177.32° | 179.949374° | — | — | 179.997119° |
| $R_{180}$ | 0.00410 | 0.566667 | — | — | 0.056351 |

*$S_T$ pour Pantheon+ est calculé par fenêtre glissante (largeur 11), méthodologie différente des autres pipelines — voir §2.3.

### 5.3 Le rôle discriminant des observables angulaires

Le résultat le plus structurant de cette partie est la **capacité des observables angulaires** ($\theta_{\rm mean}$, $R_{180}$) **à distinguer des classes de systèmes complètement différentes** :

- **Trajectoires dynamiques lisses** (Lorenz, Rössler, Duffing, Gravity Train) : $\theta_{\rm mean} < 3°$, $R_{180}=0$ — forte continuité directionnelle.
- **Bruit isotrope pur** (CMB synthétique) : $\theta_{\rm mean}\approx90°$ — aucune direction privilégiée, comme attendu pour un champ gaussien aléatoire non corrélé. C'est un excellent **cas de contrôle nul**.
- **Positions célestes ordonnées par redshift** (Pantheon+) : $\theta_{\rm mean}\approx73°$, $R_{180}$ très faible — proche de l'isotropie mais pas totalement aléatoire.
- **Séries observationnelles bruitées dans leur propre espace d'observable** (H(z)) : $\theta_{\rm mean}\approx116°$, $R_{180}\approx0.57$ — plus de la moitié des incréments sont quasi-opposés, signature d'un zigzag caractéristique des données bruitées à faible nombre de points.

Cette hiérarchie ($\theta_{\rm mean}$ : dynamique lisse ≪ Pantheon+ < CMB bruit ≪ H(z)$) constitue une piste concrète pour utiliser GVH Dynamic comme **classificateur géométrique** de la nature d'un signal, indépendamment de son interprétation physique.

### 5.4 Limites à noter

- Le pipeline **CMB** utilise une carte synthétique (bruit gaussien, non une vraie carte Planck) : les résultats valident le fonctionnement du pipeline, pas une propriété cosmologique réelle.
- Le pipeline **BAO** repose sur un très petit nombre de points par série, ce qui explique la valeur identique $R_{\rm super}=0.333$ pour les deux observables — probable artefact de faible échantillon, et absence d'observables angulaires calculables.

---

## 6. Synthèse transversale

### 6.1 Tableau global (les huit systèmes)

| Système | Catégorie | $\theta_{\rm mean}$ | $R_{180}$ | $S_T^{\rm norm}$ |
|---|---|---|---|---|
| Lorenz | Chaos | 2.43° | 0 | 0.6057 |
| Rössler | Chaos | 0.72° | 0 | 0.9187 |
| Duffing | Chaos forcé | 1.75° | 0 | 0.6952 |
| Gravity Train (A) | Référence analytique | 0.090026° | 0 | 0.2505 |
| Gravity Train (B) | Référence analytique | 0.114299° | 0 | 0.4729 |
| Pantheon+ | Cosmologie (position céleste) | 73.22° | 0.0041 | — |
| H(z) | Cosmologie (série bruitée) | 116.48° | 0.5667 | 0.9791 |
| BAO | Cosmologie (série courte) | n/a | n/a | — |
| CMB (synthétique) | Bruit de contrôle | 90.16° | 0.0564 | — |

### 6.2 Ce que GVH Dynamic 0.1 démontre

1. **Un même cadre géométrique général s'applique à l'ensemble des pipelines**, avec certaines conventions opératoires encore spécifiques aux jeux de données dans la version 0.1 (définitions de $D_c$, $A_H$, $B_H$ — voir §2.3) — validant la faisabilité méthodologique du projet, sans encore prouver une universalité stricte des observables.
2. **Les observables angulaires ($\theta_{\rm mean}$, $R_{180}$) séparent nettement** les trajectoires dynamiques lisses, le bruit isotrope, et les séries observationnelles bruitées.
3. **GVH Dynamic détecte des changements de régime physique connus** (rupture d'invariance harmonique du Gravity Train), ce qui constitue une validation de sensibilité du cadre.
4. **La dispersion multi-échelle et la loi hiérarchique ($S_T^{\rm norm}$, $B_H$) discriminent entre systèmes chaotiques** de nature différente, même quand les signatures angulaires sont proches.

### 6.3 Ce que GVH Dynamic 0.1 ne démontre pas (et ne prétend pas démontrer)

- Aucune interprétation physique fondamentale des observables n'est proposée ici.
- L'universalité des observables n'est pas prouvée : les définitions de $D_c$, $A_H$, $B_H$ varient encore d'un pipeline à l'autre (§2.3).
- Les résultats CMB reposent sur une carte synthétique, pas sur des données réelles.
- Les résultats chaotiques ne sont reproductibles qu'à tolérance statistique près (sensibilité aux conditions initiales), pas bit à bit.

---

## 7. Reproductibilité et environnement numérique

Tous les pipelines chaotiques ont été exécutés avec :

```
Python  : 3.12.13
NumPy   : 2.0.2
SciPy   : 1.16.3
pandas  : 2.2.2
```

Chaque pipeline exporte ses résultats et trajectoires en CSV (`GVH_<Système>_Observables_0.1.csv`, `..._Trajectory_0.1.csv`, `..._Increments_0.1.csv` pour les systèmes dynamiques ; exports équivalents pour les jeux cosmologiques), garantissant la traçabilité complète des calculs.

Un avertissement méthodologique commun à tous les notebooks : comme Lorenz, Rössler et Duffing sont des systèmes chaotiques, une reproductibilité bit à bit n'est pas garantie entre versions de solveurs numériques ; les observables GVH doivent être lues comme des quantités **statistiquement stables**, non comme des valeurs trajectorielles strictement identiques.

---

## 8. Perspectives pour GVH Dynamic 0.2

- **Standardiser** les définitions de $D_c$, $A_H$, $B_H$ à travers tous les pipelines (actuellement hétérogènes, §2.3).
- **Remplacer la carte CMB synthétique** par une vraie carte Planck.
- **Étendre BAO** à un jeu de données plus large permettant le calcul des observables angulaires.
- **Tests de robustesse** : sensibilité aux conditions initiales (Lorenz/Rössler/Duffing), au pas d'échantillonnage, et tests Monte Carlo systématiques.
- **Étude de sensibilité paramétrique** pour Gravity Train (profils de densité intermédiaires entre Modèle A et B) et pour Rössler ($a,b,c$).
- Explorer le rôle de $\theta_{\rm mean}$ et $R_{180}$ comme **classificateur géométrique générique** de la nature d'un signal (trajectoire vs. série bruitée vs. bruit isotrope), suggéré en §5.3.

---

*Ce volume est descriptif et méthodologique. Toute interprétation physique des observables GVH relève d'un cadre théorique distinct (VP–GVH) et n'entre pas dans le périmètre de GVH Dynamic 0.1.*
