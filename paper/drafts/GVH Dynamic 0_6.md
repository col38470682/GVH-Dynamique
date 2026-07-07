# GVH Dynamic 0.6 — Robustesse, invariance pratique et reproductibilité

**Statut du document**

- Version : 0.6
- Série : GVH Dynamic
- Nature : Cohérence mathématique — robustesse et invariance pratique
- Langue : Français
- Statut : Document méthodologique de référence

---

## 1. Objet

GVH Dynamic 0.1 à 0.5 a construit le vecteur d'observables :

$$
\mathcal O_{\rm GVH} = (D_T^{\rm mean}, S_T, S_T^{\rm norm}, D_c, R_{\rm super}, A_H, B_H, \theta_{\rm mean}, \theta_{\max}, R_{180}).
$$

La version 0.6 formalise les conditions sous lesquelles ce vecteur peut être considéré comme reproductible.

L'objectif est de distinguer invariance mathématique exacte de robustesse numérique observée.

---

## 2. Invariance exacte

Certaines propriétés sont démontrées par construction : $u=D/D_{\max}$ est invariant sous $X\rightarrow \lambda QX+C$ ($\lambda\neq0$, $Q^TQ=I$) ; les angles $\theta_{ij}$ sont invariants sous transformation orthogonale commune et redimensionnement positif des vecteurs.

Ces invariances sont exactes dans le cadre mathématique idéal.

---

## 3. Robustesse numérique

La robustesse numérique concerne : $\mathcal O_{\rm GVH}(X) \approx \mathcal O_{\rm GVH}(X+\varepsilon)$ lorsque la perturbation $\varepsilon$ est petite. Cette propriété n'est pas automatique. Elle doit être testée pour chaque pipeline.

---

## 4. Notion de perturbation

On considère $X_\epsilon = X + \epsilon \eta$. La stabilité d'une observable $O$ peut être évaluée par $\Delta O(\epsilon) = |O(X_\epsilon)-O(X)|$, ou en version relative $\delta O(\epsilon) = \frac{|O(X_\epsilon)-O(X)|}{|O(X)|+\varepsilon_0}$.

---

## 5. Critère pratique de robustesse

Une observable est dite robuste si $\delta O(\epsilon) \leq \tau$ pour une tolérance choisie $\tau>0$. Cette définition est pratique, non absolue.

---

## 6. Robustesse sous bruit

On construit $X_\sigma = X+\sigma \eta$ et on calcule $\mathcal O_{\rm GVH}(X_\sigma)$ pour plusieurs valeurs de $\sigma$.

---

## 7. Exemple Lorenz : stabilité de $B_H$

$$
\sigma_{\rm noise}=0.01 \Rightarrow B_H\approx0.8595, \qquad \sigma_{\rm noise}=0.05 \Rightarrow B_H\approx0.8580, \qquad \sigma_{\rm noise}=0.10 \Rightarrow B_H\approx0.8568.
$$

Ces résultats indiquent une stabilité forte de $B_H$ dans cette configuration, mais ne constituent pas une preuve générale pour tout système.

---

## 8. Robustesse sous changement de fenêtre

On compare $\mathcal O_{\rm GVH}^{(I_1)}$ et $\mathcal O_{\rm GVH}^{(I_2)}$ pour deux fenêtres $I_1$, $I_2$.

---

## 9. Exemple Lorenz–Duffing : fenêtres testées

$$
B_H^{\rm Lorenz} \in [0.8175,0.9587], \qquad B_H^{\rm Duffing} \in [1.0799,1.3853].
$$

Fenêtres testées : 50–99, 60–99, 50–95. Dans ces configurations, les plages Lorenz et Duffing restaient séparées.

---

## 10. Robustesse sous résolution

Changer $N$ peut modifier $D_T$, $S_T$, $D_c$, $R_{\rm super}$, $B_H$, $R_{180}$. Un test de résolution consiste à comparer $N$, $2N$, $4N$.

---

## 11. Sensibilité aux dérivées numériques

Différents schémas (différence avant, différence centrée, gradient numérique, lissage puis dérivation) peuvent produire des écarts. Tout pipeline reproductible doit préciser la méthode utilisée.

---

## 12. Robustesse angulaire

Les angles $\theta_{ij}$ peuvent être sensibles lorsque $|\mathbf v_i|\approx0$. Il est recommandé d'appliquer un seuil $|\mathbf v_i|>\eta$.

---

## 13. Tests Monte Carlo

On produit plusieurs réalisations $X^{(1)},\dots,X^{(M)}$ et on calcule $\mathcal O_{\rm GVH}^{(k)}$ pour chacune. On estime $\mu_O = \frac1M\sum_k O^{(k)}$ et $\sigma_O = \sqrt{\frac1{M-1}\sum_k (O^{(k)}-\mu_O)^2}$.

---

## 14. Campagne Monte Carlo Lorenz–Rössler–Duffing

$$
B_H^{\rm Lorenz} \approx 0.8586\pm0.0358, \qquad B_H^{\rm Rossler} \approx 1.1583\pm0.0963, \qquad B_H^{\rm Duffing} \approx 1.2607\pm0.0595.
$$

> **Note d'archive :** valeurs reprises de la même campagne mentionnée en 0.2 §14.2 et 0.4.

---

## 15. Séparation standardisée

$$
\Delta_{AB} = \frac{|\mu_A-\mu_B|}{\sqrt{\sigma_A^2+\sigma_B^2}}.
$$

$$
\Delta_{LR}\approx2.92\sigma, \qquad \Delta_{RD}\approx0.91\sigma, \qquad \Delta_{LD}\approx5.79\sigma.
$$

---

## 16. Contrôles négatifs

$$
B_H^{\rm sinus} \approx11.613, \quad R^2\approx0.869. \qquad\qquad B_H^{\rm bruit\ blanc} \approx0.9588, \quad R^2\approx0.993.
$$

Ces résultats montrent que la qualité d'ajustement seule ne suffit pas.

---

## 17. Reproductibilité computationnelle

Pour chaque pipeline, il faut documenter : langage ; version de Python ; versions de NumPy, SciPy, pandas ; générateurs aléatoires ; seeds ; méthode d'intégration ; tolérances numériques ; taille des grilles ; méthode de dérivation ; méthode de fit ; fenêtres utilisées.

---

## 18. Reproductibilité faible et forte

**Reproductibilité forte** : $O_{\rm reproduit} = O_{\rm référence}$ à l'arrondi près.

**Reproductibilité faible** : $|O_{\rm reproduit}-O_{\rm référence}|\leq\tau$. Plus réaliste pour les systèmes chaotiques.

---

## 19. Cas des systèmes chaotiques

Pour Lorenz et Rössler, la reproductibilité bit à bit n'est pas toujours garantie. La validation doit porter sur les plages statistiques, les tendances, les intervalles de tolérance, les observables agrégées, les contrôles.

---

## 20. Critère de validation d'un pipeline GVH

Un pipeline GVH est validé méthodologiquement si : 1) les définitions des observables sont explicites ; 2) les paramètres sont documentés ; 3) les résultats principaux sont reproductibles ; 4) les écarts sont expliqués ou bornés ; 5) les contrôles négatifs sont inclus ; 6) la dépendance aux fenêtres est testée ; 7) la sensibilité au bruit est évaluée ; 8) les limites sont formulées clairement.

---

## 21. Ce qui est démontré

- la distinction entre invariance exacte et robustesse numérique ;
- la définition de la variation absolue $\Delta O$ ;
- la définition de la variation relative $\delta O$ ;
- un critère pratique de robustesse avec tolérance ;
- un schéma Monte Carlo pour estimer moyenne et dispersion ;
- une mesure de séparation standardisée entre signatures.

---

## 22. Ce qui est soutenu numériquement

La robustesse de $B_H$ au bruit pour Lorenz dans la plage testée ; la séparation Lorenz–Duffing ; la stabilité partielle sous fenêtres ; la nécessité de contrôles négatifs ; la reproductibilité forte du pipeline Duffing final ; la reproductibilité statistique du pipeline Rössler.

---

## 23. Ce qui n'est pas démontré

La robustesse universelle de toutes les observables ; l'indépendance totale aux solveurs numériques ; l'indépendance totale aux fenêtres ; l'insensibilité à tout type de bruit ; la classification parfaite des systèmes dynamiques ; une preuve cosmologique ; une relation nécessaire avec Volume Partagé.

---

## 24. Résultat structurel de GVH Dynamic 0.6

$$
\boxed{X \rightarrow D_T \rightarrow u \rightarrow R_{\rm super} \rightarrow (A_H,B_H) \rightarrow (\theta_{\rm mean},\theta_{\max},R_{180}) \rightarrow \text{robustesse}}
$$

---

## 25. Transition vers GVH Dynamic 0.7

La version 0.7 doit rassembler les observables en un cadre diagnostique unifié :

$$
\mathcal G[X] = \mathcal O_{\rm GVH} \mapsto (D_T, S_T, S_T^{\rm norm}, D_c, R_{\rm super}, A_H, B_H, \theta_{\rm mean}, \theta_{\max}, R_{180}).
$$

---

## Conclusion

GVH Dynamic 0.6 formalise la robustesse, l'invariance pratique et la reproductibilité.

$$
\boxed{\text{observable} + \text{robustesse} + \text{contrôle} + \text{reproductibilité}}
$$

Cette version prépare le passage final vers GVH Dynamic 0.7, où l'ensemble des observables sera regroupé dans un cadre diagnostique unifié.

> **Note d'archive :** plusieurs résultats numériques de cette section (§7, 9, 14, 15, 16) reprennent des valeurs déjà présentées en 0.2 et 0.4, issues très probablement d'une seule et même campagne de calcul. Ce recyclage a été signalé dans la synthèse 0.1–0.7 comme un point à corriger (documentation de provenance ou nouvelle campagne indépendante).
