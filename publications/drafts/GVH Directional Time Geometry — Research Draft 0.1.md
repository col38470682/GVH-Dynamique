GVH Directional Time Geometry — Research Draft 0.1
Statut du document
Type : brouillon de recherche exploratoire Statut scientifique : non validé Intégration au noyau GVH : interdite à ce stade Principe de gouvernance : toute hypothèse doit être formalisée, testée numériquement, comparée à la relativité restreinte et générale, puis confrontée aux données avant toute intégration au noyau validé.
￼
1. Objectif général
Explorer une représentation géométrique dans laquelle un événement spatial
[ \overrightarrow{OP}=x\mathbf{i}+y\mathbf{j}+z\mathbf{k} ]
est associé à :
	1.	un temps propre global unique ;
	2.	une structure directionnelle interne ;
	3.	une décomposition tensorielle capable de suivre la géométrie de la trajectoire ;
	4.	une éventuelle loi de compensation entre les directions spatiales et leurs paramètres temporels.
L’objectif n’est pas de supposer que cette construction remplace la relativité, mais de déterminer si elle constitue une reparamétrisation, une reformulation géométrique utile, ou une extension physique produisant des prédictions nouvelles.
￼
2. Point de départ géométrique
Dans un espace euclidien tridimensionnel :
[ \overrightarrow{OP}=x\mathbf{i}+y\mathbf{j}+z\mathbf{k}. ]
La norme spatiale est :
[ |\overrightarrow{OP}|=\sqrt{x^2+y^2+z^2}. ]
Exemple :
[ \overrightarrow{OP}=3\mathbf{i}+5\mathbf{j}+7\mathbf{k}, ]
avec :
[ |\overrightarrow{OP}|=\sqrt{83}. ]
￼
3. Hypothèse initiale : trois temps directionnels
L’hypothèse initiale associait à chaque direction un temps propre distinct :
[ \tau_x,\qquad \tau_y,\qquad \tau_z. ]
Les premiers tests exploratoires ont montré que trois temps propres physiques totalement indépendants ne reproduisent pas directement le temps propre relativiste.
Statut
[ \boxed{\text{Hypothèse abandonnée sous sa forme indépendante.}} ]
￼
4. Reformulation : loi de compensation directionnelle
Une nouvelle hypothèse a été introduite :
[ \boxed{dx,d\tau_x=dy,d\tau_y=dz,d\tau_z=d\Lambda.} ]
Elle implique :
[ d\tau_x=\frac{d\Lambda}{dx},\qquad d\tau_y=\frac{d\Lambda}{dy},\qquad d\tau_z=\frac{d\Lambda}{dz}. ]
Cette relation exprime une compensation inverse :
[ |dx|>|dy|\Longrightarrow |d\tau_x|<|d\tau_y|. ]
Réserve
Cette loi devient singulière lorsqu’une composante spatiale s’annule. Elle ne peut donc pas constituer, sous cette forme, une loi covariante complète.
￼
5. Construction géométrique du cube
On représente les trois directions par les arêtes d’un parallélépipède rectangle :
[ dx,\qquad dy,\qquad dz. ]
La diagonale intérieure reliant deux sommets opposés est :
[ \overrightarrow{OP}=dx\mathbf{i}+dy\mathbf{j}+dz\mathbf{k}. ]
Sa longueur est :
[ d\ell=\sqrt{dx^2+dy^2+dz^2}. ]
Dans cette représentation :
	●	les arêtes portent les variables directionnelles ;
	●	la diagonale représente l’événement global ;
	●	le temps physique mesurable doit rester unique.
￼
6. Temps global reconstruit
Une première définition quadratique du temps global est :
[ \boxed{d\tau_G^2=\frac{d\tau_x^2+d\tau_y^2+d\tau_z^2}{3}.} ]
Avec la loi de compensation :
[ d\tau_G^2=\frac{d\Lambda^2}{3}\left(\frac1{dx^2}+\frac1{dy^2}+\frac1{dz^2}\right). ]
On introduit une longueur effective :
[ \boxed{L_{\mathrm{eff}}^2=\frac{3}{\frac1{dx^2}+\frac1{dy^2}+\frac1{dz^2}}.} ]
Ainsi :
[ d\tau_G^2=\frac{d\Lambda^2}{L_{\mathrm{eff}}^2}. ]
￼
7. Loi minimale pour (d\Lambda)
Une première loi autonome testée est :
[ d\Lambda=L_{\mathrm{eff}}dt. ]
Elle donne :
[ d\tau_G=dt. ]
Cette loi est cohérente mathématiquement, mais ne produit aucune dilatation temporelle. Il faut donc introduire une dépendance dynamique :
[ \boxed{d\Lambda=L_{\mathrm{eff}}dt,F!\left(\frac{v^2}{c^2}\right).} ]
￼
8. Détermination de la fonction (F)
La reconstruction donne :
[ d\tau_G=dt,F!\left(\frac{v^2}{c^2}\right). ]
Les contraintes imposées sont :
	●	(F(0)=1) ;
	●	isotropie ;
	●	invariance de (c) ;
	●	équivalence des référentiels inertiels ;
	●	cohérence de la composition relativiste des vitesses.
Ces postulats conduisent à :
[ \boxed{F(\beta)=\sqrt{1-\beta^2}.} ]
Donc :
[ \boxed{d\tau_G=dt\sqrt{1-\frac{v^2}{c^2}}.} ]
La loi de compensation devient :
[ \boxed{d\Lambda=L_{\mathrm{eff}}dt\sqrt{1-\frac{v^2}{c^2}}.} ]
Statut
Cette construction reproduit la dilatation temporelle de la relativité restreinte, mais constitue encore une reformulation directionnelle de la même cinématique.
￼
9. Échec de la décomposition inverse sous boost
La forme
[ d\tau_i=\frac{L_{\mathrm{eff}}}{dx_i}d\tau_G ]
est singulière si (dx_i=0). Or une transformation de Lorentz peut rendre nulle une composante spatiale dans un référentiel donné.
Conclusion
La loi inverse originale n’est pas covariante.
￼
10. Décomposition directionnelle régulière
On définit :
[ w_i=\frac{dx_i^2}{dx^2+dy^2+dz^2}, ]
avec :
[ w_x+w_y+w_z=1. ]
Puis :
[ \boxed{d\tau_i^2=w_i,d\tau_G^2.} ]
Ainsi :
[ \boxed{d\tau_x^2+d\tau_y^2+d\tau_z^2=d\tau_G^2.} ]
Cette écriture reste finie lorsqu’une composante spatiale est nulle.
￼
11. Tenseur directionnel spatial
On définit :
[ \mathbf n=\frac{1}{d\ell}\begin{pmatrix}dx\dy\dz\end{pmatrix}. ]
Puis :
[ \boxed{\mathbf D=d\tau_G^2,\mathbf n\mathbf n^{\mathsf T}.} ]
Ses composantes sont :
[ D_{ij}=d\tau_G^2n_in_j. ]
Sa trace vaut :
[ \boxed{\operatorname{tr}(\mathbf D)=d\tau_G^2.} ]
Sous rotation spatiale :
[ \boxed{\mathbf D’=R\mathbf D R^{\mathsf T}.} ]
Cette formulation conserve les termes croisés et se transforme correctement sous rotation.
￼
12. Limite du tenseur spatial
Sous un boost de Lorentz, le temps et l’espace se mélangent. Le tenseur spatial (3\times3) dépend donc de l’observateur et ne constitue pas un tenseur de Lorentz complet.
￼
13. Formulation covariante quadridimensionnelle
On introduit :
	●	la quadrivitesse de l’observateur (u^\mu) ;
	●	une direction spatiale locale (n^\mu).
Les contraintes sont :
[ u_\mu n^\mu=0, ]
et :
[ n_\mu n^\mu=-1 ]
pour la signature ((+,-,-,-)).
Le tenseur directionnel devient :
[ \boxed{\mathcal D^{\mu\nu}=d\tau_G^2n^\mu n^\nu.} ]
Sous transformation de Lorentz :
[ \boxed{\mathcal D’^{\mu\nu}=\Lambda^\mu{}{\alpha}\Lambda^\nu{}{\beta}\mathcal D^{\alpha\beta}.} ]
￼
14. Généralisation à l’espace-temps courbe
Dans un espace-temps courbe :
[ \boxed{c^2d\tau_G^2=g_{\mu\nu}dX^\mu dX^\nu.} ]
Le projecteur spatial associé à l’observateur est :
[ \boxed{h_{\mu\nu}=g_{\mu\nu}-\frac{u_\mu u_\nu}{c^2}.} ]
Le tenseur directionnel devient :
[ \boxed{\mathcal D^{\mu\nu}(X)=d\tau_G^2n^\mu(X)n^\nu(X).} ]
￼
15. Évolution covariante de la direction
La variation de (n^\mu) le long de la trajectoire est :
[ \frac{Dn^\mu}{d\tau_G}=u^\alpha\nabla_\alpha n^\mu. ]
Une observable géométrique possible est :
[ \boxed{\kappa_G^2=-g_{\mu\nu}\frac{Dn^\mu}{d\tau_G}\frac{Dn^\nu}{d\tau_G}.} ]
Puis :
[ \boxed{K_G=\int\kappa_G,d\tau_G.} ]
Cette quantité pourrait distinguer des trajectoires ayant le même temps propre mais des géométries différentes.
￼
16. Résultats actuels
Résultats positifs
	●	Le temps propre global est compatible avec la relativité restreinte.
	●	La fonction relativiste est retrouvée à partir des postulats inertiels.
	●	La décomposition tensorielle fonctionne sous rotation.
	●	Le temps propre global est invariant sous boost.
	●	Une formulation covariante quadridimensionnelle peut être écrite.
Résultats négatifs ou limites
	●	Trois temps propres physiques totalement indépendants ne fonctionnent pas.
	●	La loi inverse (dx,d\tau_x=d\Lambda) devient singulière.
	●	Aucune nouvelle prédiction physique n’a encore été obtenue.
	●	L’équivalence avec la relativité générale n’est pas démontrée.
	●	Le tenseur directionnel ne remplace pas la métrique ni la courbure.
￼
17. Hypothèse actuelle la plus solide
[ \boxed{\text{un temps propre global invariant}+\text{un tenseur directionnel local}.} ]
Le temps propre est :
[ \boxed{d\tau_G=dt\sqrt{1-\frac{v^2}{c^2}}.} ]
La structure directionnelle est :
[ \boxed{\mathcal D^{\mu\nu}=d\tau_G^2n^\mu n^\nu.} ]
￼
18. Prochaine étape
Calculer explicitement, dans la métrique de Schwarzschild, le transport de (n^\mu) pour :
	1.	une chute radiale ;
	2.	une orbite circulaire ;
	3.	une géodésique lumineuse.
Puis comparer (\kappa_G) dans l’espace plat et dans l’espace courbe.
￼
19. Critères de validation future
La construction devra être testée contre :
	●	les transformations de Lorentz ;
	●	les géodésiques de Schwarzschild ;
	●	la déviation de la lumière ;
	●	la précession du périhélie ;
	●	les invariants de courbure ;
	●	les données numériques ou observationnelles disponibles.
Aucune intégration au noyau GVH ne doit avoir lieu avant ces validations.
￼
20. Gouvernance scientifique
Ce document doit rester dans un dossier séparé de recherche exploratoire.
Nom recommandé :
```text GVH_Directional_Time_Geometry_Draft_0.1.md ```
Toute évolution devra distinguer clairement :
	●	intuition ;
	●	définition ;
	●	hypothèse ;
	●	dérivation ;
	●	test numérique ;
	●	résultat ;
	●	échec ;
	●	question ouverte ;
	●	statut de validation.