# GVH Dynamic 0.4 — Loi hiérarchique

**Statut du document**

- Version : 0.4
- Série : GVH Dynamic
- Nature : Cohérence mathématique — loi hiérarchique
- Langue : Français
- Statut : Document méthodologique de référence

---

## Formule centrale

$$
R_{\rm super}(u)=A_H e^{-B_Hu}
$$

où :

- $R_{\rm super}(u)$ est la fraction supercritique mesurée à un seuil normalisé $u$ ;
- $A_H$ est l'amplitude hiérarchique ;
- $B_H$ est la pente hiérarchique effective ;
- $u=D/D_{\max}$, avec $0\leq u\leq1$.

---

## Chaîne logique

GVH Dynamic 0.4 prolonge : $D_T \rightarrow u \rightarrow R_{\rm super}(u) \rightarrow (A_H,B_H)$.

La version 0.3 définissait : $R_{\rm super} = \#\{D_i>D_c\}/N$.

La version 0.4 généralise cette idée en faisant varier le seuil normalisé :

$$
R_{\rm super}(u) = \frac{\#\{i:u_i>u\}}{N}.
$$

---

## Loi hiérarchique descriptive

La décroissance de $R_{\rm super}(u)$ est ajustée par $R_{\rm super}(u)=A_H e^{-B_Hu}$.

Cette loi est une loi descriptive d'ajustement. Elle ne doit pas être présentée comme une loi physique universelle.

---

## Linéarisation

Lorsque $R_{\rm super}(u)>0$, on peut écrire :

$$
\ln R_{\rm super}(u) = \ln A_H - B_H u.
$$

Donc $B_H$ est l'opposé de la pente dans l'espace logarithmique.

---

## Interprétation de $A_H$

$A_H=R_{\rm super}(0)$ dans l'ajustement idéal.

En pratique, $A_H$ dépend de la fenêtre d'ajustement, du traitement des zéros, de la grille de seuils, de la distribution de $u$.

---

## Interprétation de $B_H$

$B_H$ mesure la vitesse de décroissance de la masse supercritique.

Si $B_H$ est grand, $R_{\rm super}(u)$ décroît rapidement. Si $B_H$ est petit, $R_{\rm super}(u)$ décroît lentement.

Ainsi, $B_H$ est une signature hiérarchique effective.

---

## Résultats numériques déjà observés

$$
B_H^{\rm Lorenz}\approx0.8586\pm0.0358, \qquad B_H^{\rm Rossler}\approx1.1583\pm0.0963, \qquad B_H^{\rm Duffing}\approx1.2607\pm0.0595.
$$

Avec :

$$
R^2_{\rm Lorenz}\approx0.986, \qquad R^2_{\rm Rossler}\approx0.985, \qquad R^2_{\rm Duffing}\approx0.965.
$$

Ces résultats montrent que $B_H$ peut différencier certains systèmes, mais pas tous.

> **Note d'archive :** ces valeurs sont reprises de la même campagne de calcul mentionnée en 0.2 §14.2 ; aucun protocole d'estimation (grille, méthode de fit, traitement des zéros) n'est spécifié dans ce document. Voir GVH Dynamic 0.8 pour le protocole formalisé ultérieurement.

---

## Limite importante

$B_H$ ne doit pas être utilisé seul comme classificateur universel.

Les contrôles ont montré qu'un bruit blanc peut aussi produire un bon ajustement exponentiel.

$$
\boxed{B_H\ \text{seul}\neq\text{preuve de chaos}} \qquad \boxed{B_H\ \text{seul}\neq\text{signature physique universelle}.}
$$

---

## Ce qui est établi

- la fonction $R_{\rm super}(u)$ ;
- la loi descriptive $A_He^{-B_Hu}$ ;
- la signification mathématique de $A_H$ ;
- la signification mathématique de $B_H$ ;
- la linéarisation logarithmique ;
- le rôle diagnostique de $B_H$.

---

## Ce qui n'est pas démontré

- l'universalité de $B_H$ ;
- l'universalité de la loi exponentielle ;
- une preuve cosmologique ;
- une preuve du modèle Volume Partagé ;
- une classification parfaite des systèmes dynamiques.

---

## Résultat structurel

$$
\boxed{X \rightarrow D_T \rightarrow u \rightarrow R_{\rm super}(u) \rightarrow (A_H,B_H)}
$$

---

## Conclusion

GVH Dynamic 0.4 formalise la loi hiérarchique :

$$
\boxed{R_{\rm super}(u)=A_H e^{-B_Hu}}
$$

Elle introduit $A_H$ et $B_H$ comme paramètres descriptifs permettant de mesurer la décroissance de la fraction supercritique.

Cette version constitue le quatrième niveau de cohérence mathématique de GVH Dynamic.

> **Note d'archive rétrospective :** cette version pose la forme fonctionnelle du modèle mais ne spécifie pas le protocole d'estimation (grille de seuils, méthode de fit, traitement des zéros, incertitudes). Ce trou méthodologique a été identifié dans la synthèse 0.1–0.7 et comblé par GVH Dynamic 0.8 (Protocole reproductible d'estimation de $A_H$ et $B_H$).
