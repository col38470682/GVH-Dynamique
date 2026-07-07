# GVH Dynamic 0.5 — Géométrie angulaire et opposition directionnelle

**Statut du document**

- Version : 0.5
- Série : GVH Dynamic
- Nature : Cohérence mathématique — géométrie angulaire
- Langue : Français
- Statut : Document méthodologique de référence

---

## 1. Objet

GVH Dynamic 0.1 à 0.4 a construit la chaîne :

$$
X \rightarrow D_T \rightarrow u \rightarrow R_{\rm super}(u) \rightarrow (A_H,B_H).
$$

Cette chaîne mesure l'intensité, la normalisation, la fraction supercritique et la décroissance hiérarchique.

La version 0.5 ajoute une information directionnelle. L'objectif est de formaliser :

$$
\mathbf v_i,\mathbf v_j \rightarrow \theta_{ij} \rightarrow (\theta_{\rm mean},\theta_{\max},R_{180}).
$$

---

## 2. Vecteurs directionnels

Soit une suite de vecteurs non nuls $\mathbf v_1,\mathbf v_2,\dots,\mathbf v_N \in\mathbb R^n$.

Ces vecteurs peuvent représenter des gradients locaux, des directions de variation, des vecteurs tangents, des résidus vectoriels, des directions reconstruites à partir d'un champ ou d'une trajectoire.

Le cadre ne fixe pas une origine physique unique pour $\mathbf v_i$.

---

## 3. Angle entre deux directions

Pour deux vecteurs non nuls $\mathbf v_i\neq0$, $\mathbf v_j\neq0$, on définit :

$$
\boxed{\theta_{ij} = \arccos\left(\frac{\mathbf v_i\cdot\mathbf v_j}{|\mathbf v_i||\mathbf v_j|}\right)}
$$

avec $0\leq\theta_{ij}\leq\pi$. En degrés : $0^\circ\leq\theta_{ij}\leq180^\circ$.

---

## 4. Cas des vecteurs nuls

Si $|\mathbf v_i|=0$ ou $|\mathbf v_j|=0$, alors l'angle $\theta_{ij}$ n'est pas défini.

Une implémentation doit exclure les vecteurs nuls, ou définir une convention explicite, ou appliquer un seuil minimal de norme.

Aucun angle calculé à partir d'un vecteur nul ne doit être interprété comme une information directionnelle réelle.

---

## 5. Observables angulaires globales

### 5.1 Angle moyen

$$
\boxed{\theta_{\rm mean} = \langle \theta_{ij}\rangle}
$$

### 5.2 Angle maximal

$$
\boxed{\theta_{\max} = \max_{i,j}\theta_{ij}}
$$

### 5.3 Ratio d'opposition $R_{180}$

Pour une tolérance angulaire $\delta>0$ :

$$
\boxed{R_{180} = \frac{\#\{(i,j):\theta_{ij}\geq \pi-\delta\}}{\#\{(i,j):\theta_{ij}\text{ défini}\}}}
$$

En degrés, avec une tolérance $\delta_\theta$ :

$$
R_{180} = \frac{\#\{(i,j):\theta_{ij}\geq180^\circ-\delta_\theta\}}{N_{\rm pairs}}.
$$

---

## 6. Propriétés immédiates

$0\leq\theta_{\rm mean}\leq\pi$, $0\leq\theta_{\max}\leq\pi$, et $0\leq R_{180}\leq1$.

---

## 7. Invariance d'échelle

Soit $\mathbf w_i=\lambda_i\mathbf v_i$, avec $\lambda_i>0$.

$$
\frac{\mathbf w_i\cdot\mathbf w_j}{|\mathbf w_i||\mathbf w_j|} = \frac{\lambda_i\lambda_j(\mathbf v_i\cdot\mathbf v_j)}{\lambda_i|\mathbf v_i|\lambda_j|\mathbf v_j|} = \frac{\mathbf v_i\cdot\mathbf v_j}{|\mathbf v_i||\mathbf v_j|}.
$$

Donc $\boxed{\theta_{ij}[\mathbf w] = \theta_{ij}[\mathbf v]}$ pour tout redimensionnement positif des vecteurs.

---

## 8. Effet d'un signe négatif

Si $\mathbf w_i=-\mathbf v_i$, alors la direction est inversée.

Pour une paire, l'angle avec inversion d'un seul vecteur devient $\theta'_{ij} = \pi-\theta_{ij}$.

Contrairement au redimensionnement positif, l'inversion de signe modifie la géométrie angulaire. Cette propriété est importante pour interpréter $R_{180}$.

---

## 9. Invariance orthogonale

Soit $\mathbf w_i=Q\mathbf v_i$, avec $Q^TQ=I$.

$\mathbf w_i\cdot\mathbf w_j = \mathbf v_i^TQ^TQ\mathbf v_j = \mathbf v_i\cdot\mathbf v_j$, et $|\mathbf w_i|=|\mathbf v_i|$.

Donc $\boxed{\theta_{ij}[\mathbf w] = \theta_{ij}[\mathbf v]}$.

Les observables $\theta_{\rm mean}$, $\theta_{\max}$, $R_{180}$ sont invariantes sous rotation ou réflexion orthogonale commune.

---

## 10. Interprétation de $\theta_{\rm mean}$

- $\theta_{\rm mean}\approx0^\circ$ : directions largement alignées ;
- $\theta_{\rm mean}\approx90^\circ$ : directions globalement orthogonales ou isotropes ;
- $\theta_{\rm mean}\approx180^\circ$ : directions fortement opposées.

Cette interprétation reste descriptive.

---

## 11. Interprétation de $\theta_{\max}$

Si $\theta_{\max}\approx180^\circ$, alors au moins une paire de directions est presque opposée. Mais une seule paire extrême ne suffit pas à conclure à une structure globale. C'est pourquoi $R_{180}$ est nécessaire.

---

## 12. Interprétation de $R_{180}$

Deux cas peuvent être distingués :

- $\theta_{\max}\approx180^\circ$, $R_{180}\approx0$ : opposition rare.
- $\theta_{\max}\approx180^\circ$, $R_{180}>0$ : opposition statistiquement présente.

---

## 13. Résultats observés dans les pipelines

Pour Lorenz : $R_{180}^{\rm Lorenz}\approx0$, avec $\theta_{\rm mean}\approx4.95^\circ$, $\theta_{\max}\approx12.62^\circ$.

Pour un bruit blanc : $R_{180}\approx0.0260$, $\theta_{\rm mean}\approx120.61^\circ$, $\theta_{\max}\approx179.44^\circ$.

Ces résultats montrent que les observables angulaires peuvent distinguer des structures que $B_H$ seul ne sépare pas toujours.

---

## 14. Résultats cosmologiques observés

Pantheon+ bruts : $\theta_{\rm mean}\approx86.211^\circ$, $\theta_{\rm median}\approx56.093^\circ$, $\theta_{\max}\approx142.707^\circ$, $R_{180}=0$.

Résidus LCDM 4D : $\theta_{\rm mean}\approx89.522^\circ$, $\theta_{\rm median}\approx89.231^\circ$, $\theta_{\max}\approx103.342^\circ$, $R_{180}=0$.

> **Note d'archive :** ces valeurs cosmologiques doivent être interprétées comme des diagnostics géométriques, non comme des preuves cosmologiques directes ; la construction exacte des vecteurs $\mathbf v_i$ pour ces jeux de données n'est pas détaillée dans ce document.

---

## 15. Rôle dans le vecteur GVH

$$
\mathcal O_{\rm GVH} = (D_T^{\rm mean}, S_T, S_T^{\rm norm}, D_c, R_{\rm super}, A_H, B_H, \theta_{\rm mean}, \theta_{\max}, R_{180}).
$$

Les observables angulaires décrivent l'organisation directionnelle, non seulement l'intensité.

---

## 16. Limites computationnelles

Le nombre de paires $(i,j)$ peut croître comme $N^2$. Des stratégies possibles : échantillonnage de paires, calcul par voisinage, réduction dimensionnelle, calcul par fenêtres, approximation statistique. Toute approximation doit être documentée.

---

## 17. Sensibilité à la dimension

Les angles en grande dimension peuvent se concentrer autour de $90^\circ$ (phénomène de concentration de la mesure), ce qui peut affecter $\theta_{\rm mean}$.

---

## 18. Sensibilité au bruit

Le bruit peut modifier les directions locales, surtout lorsque $|\mathbf v_i|$ est faible. Il est utile d'introduire un seuil $|\mathbf v_i|>\eta$.

---

## 19. Ce qui est démontré

- $0\leq\theta_{ij}\leq\pi$ ; $0\leq\theta_{\rm mean}\leq\pi$ ; $0\leq\theta_{\max}\leq\pi$ ; $0\leq R_{180}\leq1$ ;
- invariance des angles sous redimensionnement positif ;
- invariance des angles sous transformation orthogonale commune ;
- nécessité d'exclure ou traiter les vecteurs nuls.

---

## 20. Ce qui est soutenu numériquement

Les observables angulaires complètent $B_H$ ; $R_{180}$ peut distinguer certaines structures directionnelles ; bruit blanc et systèmes dynamiques peuvent présenter des signatures angulaires très différentes ; les données cosmologiques testées produisent des signatures angulaires descriptives exploitables.

---

## 21. Ce qui n'est pas démontré

Que $R_{180}$ est un classificateur universel ; que $\theta_{\max}\approx180^\circ$ implique une transition physique ; que $\theta_{\rm mean}\approx90^\circ$ implique nécessairement isotropie physique ; que les signatures angulaires sont indépendantes de la dimension ; que les signatures sont automatiquement robustes au bruit ; qu'il existe une relation nécessaire avec Volume Partagé ; qu'une signature cosmologique angulaire suffit à établir une nouvelle physique.

---

## 22. Résultat structurel de GVH Dynamic 0.5

$$
\boxed{X \rightarrow D_T \rightarrow u \rightarrow R_{\rm super}(u) \rightarrow (A_H,B_H) \rightarrow (\theta_{\rm mean},\theta_{\max},R_{180})}
$$

---

## 23. Transition vers GVH Dynamic 0.6

La version 0.6 doit formaliser la robustesse et les invariances pratiques du cadre : stabilité sous bruit, sous résolution, sous changement de fenêtre, sensibilité aux paramètres numériques, reproductibilité des observables.

$$
\mathcal O_{\rm GVH} \rightarrow \text{tests de robustesse} \rightarrow \text{diagnostic reproductible}.
$$

---

## Conclusion

GVH Dynamic 0.5 introduit la géométrie angulaire dans le cadre.

$$
\boxed{\theta_{ij} = \arccos\left(\frac{\mathbf v_i\cdot\mathbf v_j}{|\mathbf v_i||\mathbf v_j|}\right)}
$$

et les observables associées sont $\boxed{\theta_{\rm mean}, \theta_{\max}, R_{180}}$.

Cette version complète les observables d'intensité et de hiérarchie par une information directionnelle, établissant le cinquième niveau de cohérence mathématique de GVH Dynamic :

$$
\boxed{\text{intensité} + \text{hiérarchie} + \text{géométrie directionnelle}}
$$

sans introduire d'interprétation physique externe ni de dépendance nécessaire au modèle Volume Partagé.
