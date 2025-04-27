1. Diagonale à 1.0
Chaque variable se corrèle parfaitement avec elle-même : c’est ce qui donne la diagonale de « 1.0 ».

2. Forte corrélation entre variables dérivées et leurs sources
Systolic_Blood_Pressure, Diastolic_Blood_Pressure et Derived_MAP (pression artérielle moyenne) sont mutuellement corrélées autour de +0.7 / +0.8.

Derived_Pulse_Pressure (différence systolique – diastolique) corrèle positivement avec la systolique et négativement avec la diastolique.

Derived_BMI corrèle positivement avec le poids et négativement avec la taille, conformément à la formule BMI = poids/(taille²).

3. Variables « indépendantes »
Les paramètres vitaux bruts — fréquence cardiaque, fréquence respiratoire, température, saturation en oxygène — présentent des corrélations très faibles entre eux (coefficients proche de 0). Ils apportent donc chacun une information nouvelle au modèle.

4. Âge et catégorie de risque
L’âge montre une corrélation modérée (~+0.2 / +0.3) avec la Risk_Category, suggérant que les sujets plus âgés tendent vers un risque plus élevé.

On observe aussi un lien léger entre Risk_Category et MAP, ce qui pointe vers l’importance de l’hypertension dans votre score de risque.

En résumé, même dans le dataset brut :

Les dérivés (MAP, Pulse_Pressure, BMI) reflètent fidèlement leurs formules de calcul.

Les « signes vitaux » de base sont très peu redondants.

L’âge et la pression artérielle moyenne apparaissent comme des facteurs clés pour la catégorie de risque.