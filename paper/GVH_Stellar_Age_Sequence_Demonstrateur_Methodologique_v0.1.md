# GVH Stellar Age Sequence — Démonstrateur méthodologique v0.1

## Résumé

Ce document présente une synthèse revue et méthodologiquement consolidée du démonstrateur **GVH Stellar Age Sequence** fondé sur le code d’évolution stellaire **YREC**. Le résultat principal est que YREC dispose déjà, dans ses sorties physiques natives, des grandeurs énergétiques locales nécessaires à l’alimentation du pipeline GVH, en particulier la contribution nucléaire locale, sans qu’une modification du code source Fortran soit requise. La difficulté actuelle ne réside donc pas dans l’absence de la grandeur \(\epsilon_{\rm nuc}(r)\), mais dans la production d’une séquence homogène, complète et reproductible de profils internes solaires multi-âges, correctement exportés et analysés. Le démonstrateur solaire déjà obtenu valide la faisabilité numérique et physique de la chaîne de traitement GVH ; il ne valide pas encore une loi astrophysique d’évolution des observables GVH avec l’âge stellaire.

## 1. Introduction

L’objectif du travail examiné est d’évaluer si des observables GVH calculées sur des profils radiaux issus d’un code d’évolution stellaire peuvent fournir des descripteurs structurels sensibles à l’évolution interne d’une étoile de masse solaire. Le cadre étudié repose sur l’exploitation des sorties de **YREC** pour construire une séquence d’âges stellaires à masse fixée, puis pour appliquer à chaque profil le même pipeline de lecture, de normalisation et d’extraction des observables GVH.

À ce stade, il est plus exact de parler de **démonstrateur méthodologique** que de benchmark exhaustif. En effet, la chaîne de traitement a été validée sur un modèle solaire calibré et sur un sous-ensemble limité de structures internes disponibles, mais la séquence complète multi-âge nécessaire à une comparaison systématique n’a pas encore été produite ni archivée dans une forme totalement reproductible.

## 2. Base technique du démonstrateur

Le notebook audité, `GVH_Stellar_Age_Sequence_Benchmark_0.1.ipynb`, a pour fonction de :

1. récupérer et inspecter le dépôt public YREC ;
2. identifier les fichiers de sortie pertinents ;
3. lire des profils internes structurés de type `.store` ;
4. convertir les variables natives en quantités physiques utilisables ;
5. construire le profil énergétique radial destiné au pipeline GVH ;
6. calculer des observables géométriques et structurelles sur le modèle solaire final ;
7. préparer l’extension future à une séquence d’âges stellaires.

L’audit structurel du notebook confirme l’existence d’un contenu substantiel et exploitable, mais montre également que son état actuel reste intermédiaire entre carnet de développement et protocole figé.

## 3. Audit d’intégrité du notebook

L’examen direct du notebook montre qu’il contient **85 cellules** au total, dont **83 cellules de code** et **2 cellules Markdown**. Les **83 cellules de code** ont un `execution_count = null`, alors même que le fichier conserve des sorties enregistrées. Aucun message d’erreur stocké n’a été trouvé dans les sorties JSON du notebook.

Ce constat signifie que le notebook n’est pas corrompu au sens syntaxique, mais qu’il ne documente pas de manière fiable son ordre d’exécution réel. Pour un document destiné à servir de base scientifique ou archivistique, cette absence de traçabilité d’exécution constitue une limite importante de reproductibilité.

L’audit met également en évidence plusieurs problèmes techniques précis :

- une cellule de tracé et de validation utilise `solar_survival_table`, `solar_fit_table` et `solar_survival_results` avant leur création effective dans la cellule suivante ;
- la fonction `compute_radial_gvh_observables()` est définie deux fois ;
- `solar_gvh_results` est calculé deux fois dans des blocs successifs ;
- certaines sections sont dupliquées ou mal numérotées ;
- le déroulé global reste dépendant de l’état mémoire du runtime.

En conséquence, un **Run all** dans un environnement vierge provoquerait une erreur de type `NameError` dans l’état actuel du document. Le notebook valide donc la faisabilité du pipeline, mais ne peut pas encore être considéré comme une version de référence proprement reproductible.

## 4. Capacité native de YREC à fournir les grandeurs énergétiques locales

L’un des résultats les plus importants de l’analyse est que YREC calcule déjà les contributions énergétiques locales nécessaires au pipeline GVH. L’examen des sorties structurées et des routines d’écriture montre que les termes énergétiques pertinents peuvent être distingués sous la forme

\[
\epsilon_{\rm nuc},
\qquad
\epsilon_{\nu},
\qquad
\epsilon_{\rm grav}.
\]

Cette distinction est méthodologiquement décisive. Elle signifie que la construction du profil énergétique radial peut s’appuyer sur une grandeur locale déjà calculée par le solveur stellaire, au lieu de reconstruire indirectement une quantité approchée à partir de la dérivée numérique de la luminosité intégrée.

La formulation la plus prudente et la plus juste est donc la suivante :

> YREC est capable de produire directement les grandeurs énergétiques locales nécessaires à l’analyse GVH des profils internes stellaires, notamment la contribution nucléaire locale, sans reconstruction par dérivation numérique de la luminosité intégrée et sans modification du code source Fortran, à condition d’activer les options de sortie physique appropriées au cas étudié.

Cette formulation doit être préférée à toute affirmation trop générale sur une combinaison universelle de drapeaux de namelist. Les paramètres exacts peuvent varier selon la version de YREC, le type de run et la convention de sortie utilisée.

## 5. Construction du profil énergétique GVH

Dans le protocole retenu, la production nucléaire spécifique exportée par YREC est convertie en production volumique selon

\[
\epsilon_V(r)=\rho(r)\,\epsilon_{\rm nuc}(r).
\]

Le profil est ensuite normalisé par sa valeur maximale :

\[
u_E(r)=\frac{\epsilon_V(r)}{\epsilon_{V,\max}}.
\]

L’observable locale fondamentale utilisée dans le pipeline GVH est alors

\[
D_T(r)=\left|\frac{du_E}{d(r/R_\star)}\right|.
\]

Cette construction présente un avantage important : elle repose directement sur une grandeur physique locale fournie par le code d’évolution, sans passer par l’approximation

\[
\epsilon \approx \frac{dL}{dm},
\]

laquelle pourrait amplifier le bruit numérique du maillage, brouiller la séparation entre contributions énergétiques et dégrader l’interprétation du bilan local lorsque les termes gravitationnels ou neutrino deviennent non négligeables.

## 6. Validation actuelle sur le modèle solaire

Le démonstrateur solaire analysé fournit un premier contrôle de cohérence énergétique. Les sorties du notebook rapportent une luminosité nucléaire intégrée

\[
L_{\rm nuc}=3.828942\times10^{33}\ {\rm erg\,s^{-1}},
\]

et une luminosité de surface

\[
L_{\star}=3.841924\times10^{33}\ {\rm erg\,s^{-1}}.
\]

L’écart relatif correspondant est de l’ordre de

\[
\frac{|L_{\rm nuc}-L_{\star}|}{L_{\star}}\approx 0.3379\%.
\]

Ce résultat constitue une validation opérationnelle de la lecture des sorties physiques et de leur conversion dans le pipeline GVH.

Après interpolation sur une grille radiale uniforme de **5000 points**, le profil solaire final fournit notamment

\[
D_{T,\max}\approx 9.467157,
\qquad
\frac{r(D_{T,\max})}{R_\star}\approx 0.056011.
\]

La courbe de survie des gradients est définie par

\[
R_{\rm super}(d)=\Pr(D_T>d),
\]

et ajustée sur sa branche intermédiaire sous forme exponentielle :

\[
R_{\rm super}(d)\approx A_H e^{-B_H d}.
\]

Pour le modèle solaire étudié, le notebook donne

\[
A_H\approx 0.237643,
\qquad
B_H\approx 0.199095,
\qquad
R^2_{\log}\approx 0.947705.
\]

Ces résultats montrent que le pipeline GVH sait extraire une signature structurelle compacte et numériquement cohérente à partir de sorties physiques natives de YREC.

## 7. Portée scientifique du résultat actuel

L’interprétation correcte de ces résultats doit rester prudente. À ce stade, le travail démontre que :

1. YREC fournit les variables locales nécessaires ;
2. ces profils peuvent être convertis dans une représentation GVH uniforme ;
3. les observables GVH peuvent être calculées automatiquement ;
4. la cohérence énergétique d’un modèle solaire peut être contrôlée ;
5. une signature structurelle peut être extraite de façon stable sur au moins un cas physique réaliste.

En revanche, le travail **ne démontre pas encore** que les observables GVH suivent une loi astrophysique robuste d’évolution avec l’âge stellaire.

Cette distinction est essentielle. Les quantités \(A_H\), \(B_H\), \(S_T\), \(S_T^{\rm norm}\) et les observables apparentées doivent, pour l’instant, être considérées comme des **descripteurs géométriques calculés sur des profils physiques**, et non comme des paramètres astrophysiques déjà établis. Leur interprétation physique, leur stabilité inter-code et leur pouvoir discriminant restent à évaluer quantitativement.

Lorsqu’une portée interprétative plus forte sera testée, ces quantités devront d’abord être envisagées comme des **descripteurs susceptibles de devenir des candidats diagnostics**, et non comme des diagnostics astrophysiques établis.

## 8. Limites actuelles du démonstrateur

### 8.1 Séquence multi-âge incomplète

Le dépôt public YREC ne fournit pas directement une séquence complète et homogène de profils internes solaires couvrant tous les âges cibles du projet. Les fichiers `.track` décrivent utilement l’évolution temporelle de grandeurs globales, mais ils ne suffisent pas à l’analyse GVH, qui requiert des profils radiaux détaillés.

Les fichiers `.store` ou `.last` contiennent ces profils structurés, mais la séquence actuellement accessible dans le run examiné demeure incomplète au regard de la grille d’âges souhaitée :

\[
0.5,\quad 1,\quad 2,\quad 4.7,\quad 7,\quad 9\ {\rm Gyr}.
\]

Les profils manquants doivent donc être produits explicitement par de nouveaux runs YREC configurés pour sauvegarder les structures internes aux âges choisis.

### 8.2 Reproductibilité interne du notebook

Le notebook conserve une valeur méthodologique réelle, mais il n’a pas encore le niveau de nettoyage requis pour une diffusion comme référence technique finale. Avant archivage, il devra être :

1. réordonné ;
2. dédupliqué ;
3. renuméroté ;
4. exécuté intégralement depuis un runtime vierge ;
5. sauvegardé avec des compteurs d’exécution et des sorties cohérents avec l’exécution réelle.

Sans cette étape, le document reste partiellement un journal de développement et non un artefact scientifique finalisé.

## 9. Reproductibilité inter-code et reproductibilité mathématique

L’un des points forts du cadre GVH est qu’il ne dépend pas de la structure logicielle interne de YREC. Les observables sont définies à partir de profils radiaux continus — par exemple \(\rho(r)\), \(\epsilon(r)\), \(T(r)\) ou d’autres champs structuraux équivalents — et non à partir d’objets internes propres à un solveur particulier.

En principe, tout code d’évolution stellaire produisant des profils compatibles peut alimenter le même pipeline GVH sans qu’il soit nécessaire de modifier les définitions mathématiques des observables. Cela inclut potentiellement des codes tels que **MESA**, **CESAM**, **GARSTEC**, **ASTEC**, **FRANEC** ou **GENEC**.

Les définitions mathématiques des observables GVH sont indépendantes du solveur numérique utilisé. Une fois les profils radiaux disponibles sous une forme compatible, leur calcul est entièrement déterminé par les équations du pipeline et ne dépend pas des structures internes propres au code d’évolution.

Cette propriété doit être soulignée : GVH se comporte ici comme une **couche d’analyse indépendante du solveur**, et non comme un ensemble de descripteurs ad hoc spécifique à YREC.

## 10. Généralité du cadre GVH

Le démonstrateur stellaire s’inscrit dans un programme plus large de déploiement des observables GVH sur des familles de systèmes de nature différente. Selon l’état du projet décrit dans les échanges préparatoires, des définitions GVH apparentées ont déjà été utilisées sur des systèmes dynamiques et sur des jeux de données cosmologiques, avant d’être adaptées ici à des profils radiaux issus de modèles d’évolution stellaire.

Les applications réalisées suggèrent que GVH peut constituer un cadre descriptif transversal applicable à plusieurs familles de données physiques. L’étendue de cette généralité devra toutefois être évaluée par des validations spécifiques à chaque domaine.

## 11. Protocole scientifique recommandé

Le travail peut désormais être organisé selon deux niveaux de validation.

### Niveau 1 — Validation technique

Pour chaque run YREC, il convient de :

- vérifier la présence effective des profils internes ;
- confirmer que les termes énergétiques sont non nuls et physiquement plausibles ;
- contrôler les unités et les conventions de signe ;
- reconstruire le bilan énergétique global ;
- vérifier l’absence de valeurs non physiques ;
- tester la stabilité numérique de l’interpolation et du calcul des observables GVH.

### Niveau 2 — Validation scientifique

À masse et configuration physique fixées, il conviendra ensuite de :

- calculer les observables GVH à plusieurs âges ;
- comparer \(r(D_{T,\max})\), \(D_{T,\max}\), \(S_T^{\rm norm}\), \(A_H\), \(B_H\) et \(1/B_H\) ;
- tester leur convergence numérique ;
- évaluer leur sensibilité à l’âge ;
- confronter les tendances observées à des propriétés connues de l’évolution du cœur stellaire ;
- reproduire l’analyse avec au moins un autre code d’évolution stellaire.

Ce n’est qu’après cette double validation que le démonstrateur pourra évoluer vers un benchmark scientifique pleinement fondé.

## 12. Acquis de la première partie

La première partie du travail établit les points suivants :

- validation du pipeline d’extraction ;
- validation des conversions physiques ;
- validation de la cohérence énergétique ;
- validation du calcul des observables GVH ;
- validation de la reproductibilité interne du pipeline, sous réserve du nettoyage final du notebook ;
- démonstration que YREC fournit déjà les grandeurs nécessaires à l’analyse.

En revanche, cette première partie n’établit pas encore :

- que GVH est plus performant que les diagnostics stellaires classiques ;
- que les observables GVH évoluent de manière monotone avec l’âge ;
- qu’elles discriminent de manière robuste différentes phases évolutives ;
- qu’elles sont indépendantes du code d’évolution employé au niveau des résultats physiques ;
- qu’elles possèdent une interprétation astrophysique unique.

## 13. Conclusion générale

L’analyse revue du notebook et des sorties physiques de YREC conduit à une conclusion nette : **le problème principal n’est pas l’absence de la grandeur nucléaire locale dans YREC, mais la constitution d’une séquence homogène et reproductible de modèles multi-âges permettant d’évaluer la sensibilité réelle des observables GVH à l’évolution stellaire**.

Le démonstrateur solaire actuel valide donc une **méthode d’extraction et de caractérisation structurelle**. Il montre que la chaîne de traitement fonctionne, que la cohérence énergétique est raisonnablement contrôlée, et qu’une signature GVH exploitable peut être extraite à partir de sorties natives du code.

En revanche, il ne valide pas encore une loi astrophysique d’évolution des paramètres GVH. Les observables GVH doivent donc, à ce stade, être considérées comme des descripteurs structurels calculés sur des profils physiques, et non comme des diagnostics astrophysiques établis.

## 14. Transition vers la seconde phase

La seconde phase du projet n’aura plus pour objectif principal de valider l’infrastructure du pipeline, mais d’évaluer la portée scientifique des observables GVH. Elle devra déterminer si ces observables évoluent de manière systématique avec l’âge, si elles corrèlent avec des diagnostics stellaires classiques, si elles apportent une information complémentaire ou redondante, et si les tendances obtenues sont robustes vis-à-vis du code d’évolution utilisé.

## 15. Formulation-clef à conserver

> Le résultat actuel valide une méthode d’extraction et de caractérisation structurelle ; il ne valide pas encore une loi astrophysique d’évolution des paramètres GVH.

## Références minimales

1. Notebook principal : `GVH_Stellar_Age_Sequence_Benchmark_0.1.ipynb`
2. Version Markdown revue : `GVH_Stellar_Age_Sequence_Demonstrateur_Methodologique_v0.1.md`
3. Référentiel YREC utilisé : dépôt GitHub officiel de YREC
4. Futures archives recommandées : dépôt GitHub du projet GVH, versionné et horodaté
