# GVH Dynamic 0.2 — Normalisation et comparabilité inter-systèmes

**Statut du document**

- Version : 0.2
- Série : GVH Dynamic
- Nature : Cohérence mathématique — normalisation
- Langue : Français
- Statut : Document méthodologique de référence

---

## 1. Objet

GVH Dynamic 0.1 a établi le noyau différentiel minimal :

$$
X \longrightarrow D_T \longrightarrow S_T.
$$

avec, pour une trajectoire $X(t) \in \mathbb R^n$,

$$
D_T(t) = \left| \frac{dX}{dt} \right|, \qquad S_T(t) = \left| \frac{dD_T}{dt} \right|.
$$

Cette construction fournit des observables locales positives, mais les valeurs brutes dépendent généralement :

- de l'amplitude du système ;
- des unités choisies ;
- de l'échelle numérique ;
- de la fenêtre d'observation ;
- de la représentation du système.

La version 0.2 introduit donc une normalisation interne destinée à construire une variable sans dimension et à améliorer la comparabilité entre systèmes.

Le choix de référence est :

$$
\boxed{u(t) = \frac{D_T(t)}{D_{\max}}}
$$

où $D_{\max} = \max_{t\in I} D_T(t)$.

La chaîne devient :

$$
X \longrightarrow D_T \longrightarrow u \longrightarrow \mathcal O_{\rm GVH}^{\rm norm}.
$$

---

## 2. Motivation mathématique

Considérons une transformation d'amplitude : $Y(t) = \lambda X(t)$, avec $\lambda \neq 0$.

D'après GVH Dynamic 0.1 : $D_T[Y] = |\lambda| D_T[X]$.

Ainsi, deux trajectoires géométriquement semblables mais exprimées à des amplitudes différentes peuvent produire des valeurs brutes différentes de $D_T$.

Cette dépendance motive l'introduction d'une coordonnée interne normalisée.

---

## 3. Définition de la variable normalisée

Soit $D_T : I \rightarrow \mathbb R_{\geq 0}$. On définit $D_{\max} = \max_{t\in I} D_T(t)$.

Sous l'hypothèse $D_{\max} > 0$, la variable normalisée est :

$$
\boxed{u(t) = \frac{D_T(t)}{D_{\max}}}
$$

Cette variable constitue la coordonnée normalisée de référence de GVH Dynamic 0.2.

---

## 4. Domaine de $u$

Puisque $0 \leq D_T(t) \leq D_{\max}$, on obtient :

$$
\boxed{0 \leq u(t) \leq 1}
$$

Ainsi : $u : I \rightarrow [0,1]$.

Cette propriété transforme des amplitudes dynamiques potentiellement très différentes en une coordonnée commune bornée.

---

## 5. Cas dégénéré

Si $D_{\max} = 0$, alors $D_T(t) = 0 \ \forall t \in I$.

Le système est alors stationnaire relativement à l'observable différentielle considérée.

Dans ce cas, l'expression $u = D_T/D_{\max}$ n'est pas définie. La convention de calcul doit donc distinguer explicitement ce cas.

Aucune division par zéro ne doit être interprétée comme une observable physique ou géométrique.

---

## 6. Invariance sous changement global d'amplitude

Considérons $Y(t) = \lambda X(t)$, $\lambda \neq 0$.

Alors $D_T[Y] = |\lambda| D_T[X]$, et $D_{\max}[Y] = |\lambda| D_{\max}[X]$.

Par conséquent :

$$
u_Y(t) = \frac{D_T[Y]}{D_{\max}[Y]} = \frac{|\lambda| D_T[X]}{|\lambda| D_{\max}[X]}.
$$

Ainsi : $\boxed{u_Y(t) = u_X(t)}$ pour tout $\lambda \neq 0$.

**Résultat.** La variable normalisée $u$ est invariante sous multiplication globale non nulle de la trajectoire par un scalaire. Cette propriété constitue le résultat mathématique central de GVH Dynamic 0.2.

---

## 7. Compatibilité avec les translations

Soit $Y(t) = X(t) + C$, $C \in \mathbb R^n$ constant.

D'après GVH Dynamic 0.1 : $D_T[Y] = D_T[X]$, donc $D_{\max}[Y] = D_{\max}[X]$.

Par conséquent : $\boxed{u_Y = u_X}$.

La normalisation conserve donc l'invariance par translation constante déjà présente au niveau de $D_T$.

---

## 8. Compatibilité avec les transformations orthogonales

Soit $Y(t) = QX(t)$, $Q^TQ = I$.

Alors $D_T[Y] = D_T[X]$, donc $D_{\max}[Y] = D_{\max}[X]$.

Ainsi : $\boxed{u_Y = u_X}$.

La variable $u$ est donc compatible avec les rotations et réflexions orthogonales de l'espace d'état lorsque la norme euclidienne est utilisée.

---

## 9. Proposition de cohérence

**Proposition 0.2-A.** Soit $X : I \rightarrow \mathbb R^n$ une trajectoire différentiable telle que $D_{\max}[X] > 0$. Pour toute transformation $Y(t) = \lambda QX(t) + C$, où $\lambda \neq 0$, $Q^TQ = I$, et $C \in \mathbb R^n$, on a :

$$
\boxed{u_Y(t) = u_X(t)} \quad \text{pour tout } t \in I.
$$

**Démonstration.** On a $\dot Y(t) = \lambda Q \dot X(t)$. Donc $D_T[Y] = |\lambda Q \dot X(t)|$. Par homogénéité de la norme : $D_T[Y] = |\lambda| |Q\dot X(t)|$. Comme $Q$ est orthogonale : $|Q\dot X(t)| = |\dot X(t)|$. Ainsi $D_T[Y] = |\lambda| D_T[X]$. Par conséquent $D_{\max}[Y] = |\lambda| D_{\max}[X]$. Donc $u_Y(t) = \frac{|\lambda| D_T[X]}{|\lambda| D_{\max}[X]} = u_X(t)$, ce qui établit la proposition. $\blacksquare$

---

## 10. Observable secondaire normalisée

Une quantité agrégée normalisée est définie par :

$$
\boxed{S_T^{\rm norm} = \frac{S_T}{D_T^{\rm mean}}}
$$

lorsque $D_T^{\rm mean} > 0$.

Cette quantité est distincte de la coordonnée locale $u(t) = D_T(t)/D_{\max}$. Le premier est une coordonnée locale normalisée. Le second est un rapport agrégé destiné à comparer l'intensité secondaire à l'échelle moyenne primaire.

---

## 11. Propriété d'échelle de $S_T^{\rm norm}$

Sous $Y(t) = \lambda X(t)$, on a $D_T[Y] = |\lambda| D_T[X]$, donc $D_T^{\rm mean}[Y] = |\lambda| D_T^{\rm mean}[X]$.

Par ailleurs, $S_T[Y] = |\lambda| S_T[X]$ (pour $\lambda$ constant).

Ainsi : $S_T^{\rm norm}[Y] = \frac{|\lambda| S_T[X]}{|\lambda| D_T^{\rm mean}[X]}$.

Donc : $\boxed{S_T^{\rm norm}[Y] = S_T^{\rm norm}[X]}$ sous changement global constant d'amplitude.

Cette propriété renforce la cohérence de la normalisation GVH.

---

## 12. Normalisation et comparabilité

La normalisation ne signifie pas que deux systèmes deviennent identiques. Elle signifie uniquement qu'ils peuvent être projetés sur un domaine commun $u \in [0,1]$.

Pour deux systèmes $X_A(t)$ et $X_B(t)$, on peut construire $u_A = D_A/D_{A,\max}$ et $u_B = D_B/D_{B,\max}$.

Les amplitudes absolues peuvent être très différentes ($D_{A,\max} \neq D_{B,\max}$), tout en permettant une comparaison sur $[0,1]$.

---

## 13. Application aux systèmes dynamiques de référence

La cohérence computationnelle de GVH Dynamic a été testée sur trois systèmes non linéaires distincts : système de Lorenz, système de Rössler, oscillateur de Duffing.

Ces trois systèmes possèdent des structures dynamiques différentes.

La normalisation commune permet d'étudier leurs signatures GVH sans imposer une amplitude brute identique.

---

## 14. Résultats comparatifs déjà obtenus

Les tests GVH antérieurs ont montré que la normalisation ne supprime pas toute information discriminante.

### 14.1 Valeurs normalisées historiques de $B_H$

Dans une première phase de normalisation :

$$
B_{\rm GVH,norm} \approx 2.7113, \qquad B_{\rm Lorenz,norm} \approx 5.0215, \qquad B_{\rm Duffing,norm} \approx 2.1389.
$$

### 14.2 Campagne Monte Carlo ultérieure

$$
B_H^{\rm Lorenz} \approx 0.8586 \pm 0.0358, \qquad B_H^{\rm Rossler} \approx 1.1583 \pm 0.0963, \qquad B_H^{\rm Duffing} \approx 1.2607 \pm 0.0595.
$$

Qualités d'ajustement associées :

$$
R^2_{\rm Lorenz} \approx 0.986, \qquad R^2_{\rm Rossler} \approx 0.985, \qquad R^2_{\rm Duffing} \approx 0.965.
$$

> **Note d'archive :** ces valeurs numériques n'étaient accompagnées, au moment de la rédaction, d'aucun protocole d'estimation explicite (grille de seuils, méthode de fit, traitement des zéros). Voir GVH Dynamic 0.8 pour le protocole formalisé ultérieurement.

---

## 15. Séparation inter-systèmes observée

$$
\Delta_{LR} \approx 2.92\sigma, \qquad \Delta_{RD} \approx 0.91\sigma, \qquad \Delta_{LD} \approx 5.79\sigma.
$$

où $L$ = Lorenz, $R$ = Rössler, $D$ = Duffing.

Ces résultats indiquent une séparation notable entre Lorenz et Rössler, une séparation faible entre Rössler et Duffing, une séparation forte entre Lorenz et Duffing.

Ils ne démontrent pas une classification universelle.

---

## 16. Robustesse par fenêtres

$$
B_H^{\rm Lorenz} \in [0.8175, 0.9587], \qquad B_H^{\rm Duffing} \in [1.0799, 1.3853].
$$

pour les fenêtres étudiées : 50–99, 60–99, 50–95.

Ce résultat soutient une stabilité empirique partielle de la signature, sans constituer une preuve d'invariance universelle aux fenêtres.

---

## 17. Robustesse au bruit

Pour Lorenz :

$$
\sigma_{\rm noise}=0.01 \Rightarrow B_H\approx0.8595, \qquad \sigma_{\rm noise}=0.05 \Rightarrow B_H\approx0.8580, \qquad \sigma_{\rm noise}=0.10 \Rightarrow B_H\approx0.8568.
$$

Ces résultats montrent une stabilité numérique remarquable dans la configuration testée, mais ne permettent pas de conclure à une invariance générale sous bruit arbitraire.

---

## 18. Contrôles

**Sinus pur** : $B_H \approx 11.613$, avec $R^2 \approx 0.869$.

**Bruit blanc** : $B_H \approx 0.9588$, avec $R^2 \approx 0.993$.

Ces contrôles montrent que $B_H$ ne doit pas être interprété isolément comme un identifiant universel de chaos ou de dynamique non linéaire. Une valeur proche entre deux systèmes ne démontre pas leur équivalence dynamique.

---

## 19. Distinction entre normalisation et classification

$$
\boxed{\text{normalisation} \neq \text{classification}} \qquad \boxed{B_H\ \text{seul} \neq \text{classificateur universel}}
$$

La classification éventuelle doit reposer sur un vecteur d'observables.

---

## 20. Vecteur normalisé d'observables

$$
\mathcal O_{\rm GVH} = \left(D_T^{\rm mean}, S_T, S_T^{\rm norm}, D_c, R_{\rm super}, A_H, B_H, \theta_{\rm mean}, \theta_{\max}, R_{180}\right).
$$

- **Quantités brutes** : $D_T^{\rm mean}$, $S_T$, $D_c$.
- **Quantités relatives ou normalisées** : $u$, $S_T^{\rm norm}$, $R_{\rm super}$, $R_{180}$.
- **Paramètres d'ajustement** : $A_H$, $B_H$.
- **Observables angulaires** : $\theta_{\rm mean}$, $\theta_{\max}$.

---

## 21. Dépendance à la fenêtre d'observation

$D_{\max} = \max_{t\in I} D_T(t)$ dépend explicitement du domaine $I$. Si $I_1 \neq I_2$, alors $D_{\max}^{(I_1)} \neq D_{\max}^{(I_2)}$ est possible, donc $u^{(I_1)} \neq u^{(I_2)}$.

La normalisation n'est donc pas universellement indépendante de la fenêtre d'observation.

---

## 22. Sensibilité aux valeurs extrêmes

Si une observation extrême produit $D_{\max} \gg D_T(t)$ pour la majorité des points, alors $u(t)$ peut comprimer fortement la distribution dans une région proche de zéro.

La normalisation max peut être sensible aux valeurs aberrantes, aux événements rares, au bruit impulsif, aux erreurs numériques extrêmes.

---

## 23. Alternatives possibles non retenues comme référence 0.2

- Normalisation par moyenne : $u_{\rm mean} = D_T / \langle D_T \rangle$.
- Normalisation min-max : $u_{\rm minmax} = (D_T - D_{\min})/(D_{\max}-D_{\min})$.
- Normalisation quadratique : $u_{\rm rms} = D_T / \sqrt{\langle D_T^2 \rangle}$.
- Normalisation robuste : $u_q = D_T / Q_q(D_T)$.

Le choix figé reste $u = D/D_{\max}$, afin de préserver la cohérence avec les pipelines déjà réalisés.

---

## 24. Formulation discrète

$$
D_{\max} = \max_{1\leq i\leq N} D_i, \qquad u_i = \frac{D_i}{D_{\max}}.
$$

```python
D_max = np.max(D)
if D_max > 0:
    u = D / D_max
else:
    u = np.zeros_like(D)
```

Le choix de retourner un vecteur nul dans le cas dégénéré est une convention numérique, à documenter.

---

## 25. Conditions de comparaison reproductible

Une comparaison entre deux systèmes doit documenter au minimum :

1. la définition exacte de $D_T$ ;
2. la norme utilisée ;
3. la fenêtre d'observation ;
4. la résolution temporelle ou spatiale ;
5. la méthode de dérivation numérique ;
6. la définition de $D_{\max}$ ;
7. le traitement des valeurs extrêmes ;
8. le traitement du cas $D_{\max}=0$ ;
9. les paramètres du système ;
10. l'environnement numérique lorsque la dynamique est chaotique.

---

## 26. Résultat structurel de GVH Dynamic 0.2

$$
\boxed{X \rightarrow D_T \rightarrow u \rightarrow \mathcal O_{\rm GVH}^{\rm norm}}
$$

avec $\boxed{u \in [0,1]}$ et invariance sous $X \rightarrow \lambda QX + C$, pour $\lambda \neq 0$, $Q^TQ = I$.

---

## 27. Ce qui est démontré

- $u \in [0,1]$ ;
- invariance de $u$ sous translation constante ;
- invariance de $u$ sous transformation orthogonale ;
- invariance de $u$ sous changement global non nul d'amplitude ;
- invariance de $S_T^{\rm norm}$ sous changement global constant d'amplitude ;
- compatibilité de la normalisation avec une comparaison inter-systèmes sur un domaine commun.

---

## 28. Ce qui est soutenu numériquement

- la persistance de signatures distinctes après normalisation ;
- une séparation notable entre Lorenz et Duffing ;
- une séparation intermédiaire entre Lorenz et Rössler ;
- une séparation faible entre Rössler et Duffing ;
- une stabilité partielle sous variation de fenêtres ;
- une stabilité de $B_H$ sous les niveaux de bruit testés pour Lorenz.

Ces résultats sont numériques et ne doivent pas être présentés comme des théorèmes universels.

---

## 29. Ce qui n'est pas démontré

- l'universalité de $u$ comme représentation optimale ;
- l'indépendance à toute reparamétrisation temporelle ;
- l'indépendance à toute fenêtre d'observation ;
- l'insensibilité universelle aux valeurs aberrantes ;
- l'universalité de $B_H$ ;
- une classification parfaite de Lorenz, Rössler et Duffing ;
- une séparation universelle entre chaos et bruit ;
- une interprétation physique fondamentale de la normalisation ;
- une relation nécessaire avec Volume Partagé.

---

## 30. Transition vers GVH Dynamic 0.3

On introduit un seuil critique $D_c$, ou $u_c$ dans l'espace normalisé, permettant de définir des régimes $D<D_c$, $D\approx D_c$, $D>D_c$.

$$
D \rightarrow D_c \rightarrow R_{\rm super}.
$$

---

## Conclusion

GVH Dynamic 0.2 introduit une couche de normalisation destinée à réduire la dépendance aux amplitudes globales et à rendre possibles des comparaisons inter-systèmes.

$$
\boxed{u = \frac{D}{D_{\max}}} \qquad \boxed{0\leq u\leq1} \text{ lorsque } D_{\max}>0.
$$

Cette normalisation est mathématiquement invariante sous les transformations $X \rightarrow \lambda QX+C$, avec $\lambda\neq0$, $Q^TQ=I$.

$$
\boxed{\text{variation} \rightarrow \text{normalisation} \rightarrow \text{comparabilité}}
$$
