# GVH Dynamic 0.3 — Régimes critiques et ratio supercritique

**Statut du document**

- Version : 0.3
- Série : GVH Dynamic
- Nature : Cohérence mathématique — régimes critiques
- Langue : Français
- Statut : Document méthodologique de référence

---

## 1. Objet

GVH Dynamic 0.1 a défini la hiérarchie différentielle $X \rightarrow D_T \rightarrow S_T$.

GVH Dynamic 0.2 a introduit la normalisation $u = D_T/D_{\max}$, $0\leq u\leq1$.

La version 0.3 introduit la notion de seuil critique et de régimes dynamiques.

L'objectif est de formaliser la chaîne :

$$
D_T \rightarrow D_c \rightarrow R_{\rm super}.
$$

où $D_c$ est un seuil critique, $R_{\rm super}$ mesure la fraction d'états situés au-dessus de ce seuil, et les régimes sous-critique, critique et supercritique sont définis de manière descriptive.

---

## 2. Donnée de départ

Soit une série positive $D_T(t) \geq 0$. Dans une implémentation discrète : $D_1, D_2, \dots, D_N$.

Ces valeurs peuvent provenir d'une trajectoire dynamique, d'un champ scalaire, d'une carte, d'une série cosmologique, d'un système numérique non linéaire, ou d'un jeu de données ordonné.

Le cadre 0.3 ne dépend pas de l'origine physique de $D_T$.

---

## 3. Seuil critique $D_c$

On introduit un seuil $D_c > 0$, qui peut être défini de plusieurs manières : imposé, statistique, empirique, ou extrait d'un ajustement.

Dans GVH Dynamic 0.3, $D_c$ est traité comme un seuil descriptif, non comme une constante physique universelle.

---

## 4. Régimes fondamentaux

### 4.1 Régime sous-critique

$D_T(t) < D_c$.

### 4.2 Régime critique

$D_T(t) \approx D_c$. Dans une implémentation numérique, la notion de proximité nécessite une tolérance : $|D_T(t)-D_c|\leq\epsilon$.

### 4.3 Régime supercritique

$D_T(t) > D_c$.

---

## 5. Formulation discrète des régimes

$$
\mathcal I_{\rm sous} = \{i: D_i<D_c\}, \qquad \mathcal I_{\rm crit} = \{i: |D_i-D_c|\leq\epsilon\}, \qquad \mathcal I_{\rm super} = \{i: D_i>D_c\}.
$$

La version minimale peut ignorer la bande critique explicite.

---

## 6. Ratio supercritique $R_{\rm super}$

$$
\boxed{R_{\rm super} = \frac{\#\{i:D_i>D_c\}}{N}}
$$

Ainsi : $0 \leq R_{\rm super} \leq 1$.

---

## 7. Interprétation descriptive de $R_{\rm super}$

Le ratio mesure la fraction d'états dépassant le seuil critique.

- Si $R_{\rm super}=0$, aucun point ne dépasse $D_c$.
- Si $R_{\rm super}=1$, tous les points dépassent $D_c$.
- Si $0<R_{\rm super}<1$, le système alterne entre états sous-critiques et supercritiques.

Cette interprétation est statistique et descriptive. Elle ne suffit pas, seule, à identifier une transition physique.

---

## 8. Formulation probabiliste

Si $D$ est traité comme une variable aléatoire positive : $R_{\rm super} = \mathbb P(D>D_c) = 1-F_D(D_c)$, où $F_D$ est la fonction de répartition de $D$.

Cette formulation montre que $R_{\rm super}$ est une mesure de queue de distribution.

---

## 9. Version normalisée

Avec $u = D/D_{\max}$, on définit $u_c = D_c/D_{\max}$.

Alors $D>D_c$ équivaut à $u>u_c$, donc :

$$
R_{\rm super} = \frac{\#\{i:u_i>u_c\}}{N}.
$$

---

## 10. Invariance sous changement global d'amplitude

Soit $Y(t)=\lambda X(t)$, $\lambda\neq0$. Alors $D_Y(t)=|\lambda|D_X(t)$.

Si le seuil est transformé de manière cohérente ($D_{c,Y}=|\lambda|D_{c,X}$), alors :

$$
\boxed{R_{\rm super}[Y] = R_{\rm super}[X]}
$$

si le seuil est mis à l'échelle de façon cohérente.

---

## 11. Attention : seuil fixe non redimensionné

Si $D_Y=|\lambda|D_X$ mais que le seuil $D_c$ reste inchangé, alors $R_{\rm super}$ peut changer.

$R_{\rm super}$ n'est donc pas automatiquement invariant sous changement d'amplitude si le seuil n'est pas transformé ou normalisé. Cette distinction est essentielle.

---

## 12. Choix de $D_c$

### 12.1 Seuil absolu : $D_c=C$.

### 12.2 Seuil moyen : $D_c=\langle D\rangle$.

### 12.3 Seuil quantile : $D_c=Q_q(D)$, alors $R_{\rm super}\approx1-q$.

### 12.4 Seuil ajusté : obtenu comme paramètre caractéristique associé à une loi hiérarchique.

---

## 13. Non-universalité de $D_c$

GVH Dynamic 0.3 ne postule pas que $D_c$ est universel. En général $D_c^{(A)} \neq D_c^{(B)}$.

Le seuil dépend du système, de la variable étudiée, de la fenêtre d'observation, de la normalisation, de la résolution, du bruit, de la méthode d'estimation.

---

## 14. Rôle de la fenêtre d'observation

Si $I_1 \neq I_2$, alors $R_{\rm super}^{(I_1)} \neq R_{\rm super}^{(I_2)}$ peut se produire. Toute comparaison doit donc préciser la fenêtre utilisée.

---

## 15. Rôle de la résolution

$R_{\rm super}$ est sensible à $N$, au pas d'échantillonnage, à la méthode de dérivation, au filtrage, à l'interpolation.

---

## 16. Sensibilité au bruit

Un bruit ajouté à $X$ peut modifier $D_T$, puis $D_c$, et enfin $R_{\rm super}$. La sensibilité est particulièrement importante si beaucoup de points sont proches du seuil.

---

## 17. Bande critique

$$
R_{\rm sous} = \frac{\#\{i:D_i<D_c-\epsilon\}}{N}, \quad R_{\rm crit} = \frac{\#\{i:|D_i-D_c|\leq\epsilon\}}{N}, \quad R_{\rm super} = \frac{\#\{i:D_i>D_c+\epsilon\}}{N}.
$$

---

## 18. Forme minimale utilisée dans les pipelines

$$
R_{\rm super} = \frac{\#\{D_i>D_c\}}{N}.
$$

Cette forme doit être accompagnée de la définition exacte de $D_c$.

---

## 19. Résultats observés dans les pipelines

- Lorenz : $R_{\rm super}\approx0.148715$ dans le pipeline de référence ;
- Duffing : $R_{\rm super}$ non nul selon la configuration, avec $R_{180}=0$ dans le pipeline final ;
- CMB : $R_{\rm super}\approx0.035365$ dans le pipeline CMB ;
- Pantheon+ : $R_{\rm super}\approx0.06284$ dans le pipeline Pantheon+ ;
- BAO, H(z) : valeurs construites dans les pipelines respectifs.

Ces valeurs ne doivent pas être comparées naïvement sans tenir compte des échelles, fenêtres et définitions de $D_c$.

---

## 20. Fonction diagnostique de $R_{\rm super}$

Le rôle de $R_{\rm super}$ est de répondre : *quelle fraction du système occupe un régime intense ?*

Il ne répond pas seul à : le système est-il chaotique ? cosmologique ? viole-t-il un modèle standard ? confirme-t-il Volume Partagé ? possède-t-il une transition physique réelle ?

---

## 21. Relation avec la loi hiérarchique

La forme étudiée dans GVH Dynamic est de type :

$$
R_{\rm super}(u) \sim A_H e^{-B_H u}.
$$

La version 0.4 formalisera cette loi hiérarchique et les paramètres $A_H$, $B_H$.

---

## 22. Ce qui est démontré

$0\leq R_{\rm super}\leq1$. $R_{\rm super}$ est invariant sous changement global d'amplitude si le seuil est transformé de façon cohérente. Dans l'espace normalisé, le régime supercritique peut être défini par $u>u_c$.

---

## 23. Ce qui est soutenu numériquement

$R_{\rm super}$ varie selon les systèmes, peut distinguer des régimes d'intensité relative, complète les observables $D_T$, $S_T$, $B_H$ et les observables angulaires, est utile comme composante du vecteur GVH global.

---

## 24. Ce qui n'est pas démontré

L'universalité de $D_c$ ; l'existence d'un seuil critique physique universel ; l'universalité de $R_{\rm super}$ ; la classification complète des systèmes ; la robustesse automatique au bruit ; l'indépendance complète à la fenêtre d'observation ; une relation nécessaire avec Volume Partagé ; une preuve cosmologique à partir de $R_{\rm super}$ seul.

---

## 25. Résultat structurel de GVH Dynamic 0.3

$$
\boxed{X \rightarrow D_T \rightarrow u \rightarrow D_c \rightarrow R_{\rm super}}
$$

ou, en version normalisée : $\boxed{u \rightarrow u_c \rightarrow R_{\rm super}}$.

---

## 26. Transition vers GVH Dynamic 0.4

$$
R_{\rm super}(u) = A_H e^{-B_H u}.
$$

avec $A_H$ : amplitude hiérarchique ; $B_H$ : pente hiérarchique ; $R^2_H$ : qualité d'ajustement éventuelle.

---

## Conclusion

GVH Dynamic 0.3 formalise le passage des observables locales aux régimes critiques.

$$
\boxed{D_T \rightarrow D_c \rightarrow R_{\rm super}} \qquad \boxed{R_{\rm super} = \frac{\#\{D_i>D_c\}}{N}} \qquad \boxed{0\leq R_{\rm super}\leq1.}
$$

Cette version établit que $R_{\rm super}$ est une mesure descriptive de la fraction d'états supercritiques, et prépare directement la loi hiérarchique de GVH Dynamic 0.4, sans introduire d'interprétation physique externe ni de dépendance nécessaire au modèle Volume Partagé.
