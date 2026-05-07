Calcul VENTIS — Logiciel de prédétermination des aérothermes eau chaude
> **⚠️ AVERTISSEMENT IMPORTANT — À LIRE AVANT TOUTE UTILISATION**
>
> Ce logiciel est un **outil de prédétermination**. Les résultats qu'il fournit sont des estimations à caractère indicatif, destinées à faciliter une première sélection de produit. **Ils ne constituent en aucun cas un engagement contractuel, une garantie de performance, ni un dimensionnement définitif.**
>
> **Tout projet doit faire l'objet d'une vérification par un bureau d'études thermiques compétent avant toute commande, installation ou mise en œuvre.**
---
Clause de non-responsabilité
VENTIS et ses partenaires déclinent toute responsabilité quant aux conséquences directes ou indirectes pouvant résulter de l'utilisation de cet outil, notamment :
Erreurs de dimensionnement entraînant un sous-chauffage ou une surconsommation énergétique
Inadaptation du matériel aux conditions réelles d'installation
Non-conformité aux réglementations thermiques en vigueur (RE2020, DTU, normes EN)
Tout dommage matériel, financier ou corporel lié à une installation réalisée sur la seule base des résultats de cet outil
L'utilisateur est seul responsable de la vérification des résultats et de leur adéquation aux exigences spécifiques de son projet.
---
Objet et limites du logiciel
Ce que fait cet outil
Ce calculateur permet d'estimer, pour des conditions d'utilisation données :
La puissance thermique échangée par les aérothermes eau chaude VENTIS (gammes AC et EC)
La température de soufflage de l'air
Le débit d'eau nécessaire dans la batterie
La perte de charge hydraulique côté eau
Le niveau sonore à 5 mètres en montage mural
Conditions de validité
Les résultats sont valables uniquement dans les plages suivantes :
Paramètre	Plage valide
Température de départ fluide	40°C à 95°C
Température de retour fluide	30°C à 85°C
Écart Tdépart - Tretour	minimum 10 K
Température air entrée	0°C à 30°C
Altitude	0 à 2 000 m
Fluide	Eau pure ou eau glycolée jusqu'à 50%
En dehors de ces plages, les résultats ne sont pas fiables et ne doivent pas être utilisés.
Ce que cet outil ne fait pas
Il ne tient pas compte des pertes thermiques du bâtiment
Il ne calcule pas les besoins de chauffage du local
Il ne vérifie pas la conformité à la RE2020 ou aux DTU applicables
Il ne prend pas en compte les pertes de charge du réseau hydraulique global
Il ne dimensionne pas le générateur de chaleur (chaudière, PAC, etc.)
Il ne gère pas les configurations en réseau (batteries en parallèle ou en série)
---
Méthode de calcul
Base de données de référence
Les coefficients d'échange thermique (`k`) ont été calibrés sur mesures réalisées avec le logiciel de définition de batterie YAHTEC (Karyer Heat Exchangers), dans les conditions suivantes :
Condition haute température : 90/70°C fluide, 15°C air entrée
Géométrie réelle des batteries : pas de tubes 25×22 mm, ailettes ondulées (corrugated) pas 2,5 mm, tubes cuivre Ø 9,52 mm
Les coefficients sont appliqués fixes (calés à 90/70°C) quelle que soit la température de fonctionnement saisie.
> **Note :** Un calage à haute température (90/70°C) est favorable — il peut conduire à une légère surestimation des puissances à basse température (ex. 50/40°C). L'écart est de l'ordre de **8 à 12%** selon les modèles. Cette approche est couramment utilisée dans la profession.
Formules utilisées
Puissance thermique — Méthode DTLM (Différence de Température Log-Moyenne) :
```
Q = k × DTLM × Fcorr_fluide
DTLM = (ΔT₁ - ΔT₂) / ln(ΔT₁/ΔT₂)
ΔT₁ = T_départ - T_soufflage
ΔT₂ = T_retour - T_air_entrée
```
Calcul itératif (5 passes) pour convergence sur T_soufflage réelle.
Moteur EC — Méthode NTU-efficacité :
UA calibré à 10V (débit maximum), recalcul de l'efficacité ε à chaque tension de commande. Pas de facteur correctif empirique — la physique NTU gère la variation de débit.
Propriétés des fluides :
Cp et ρ interpolés en fonction de T_moy fluide (tables ASHRAE Fundamentals). Densité de l'air corrigée en fonction de l'altitude (loi ISA).
Pertes de charge hydrauliques :
Loi puissance calibrée par batterie : `ΔP (kPa) = R × Q_eau^n` avec coefficients R et n issus des courbes constructeur.
Indicateurs de régime hydraulique
Le régime d'écoulement côté fluide (nombre de Reynolds Re = ρ·v·D/μ) est calculé en temps réel :
Couleur cellule	Re	Signification
Vert	Re > 5 000	Régime turbulent confirmé — calcul Gnielinski fiable
(sans couleur)	2 300 < Re < 5 000	Régime transitoire — résultat indicatif, précision ±15%
Rouge	Re < 2 300	Régime laminaire — résultat non garanti, à vérifier impérativement
En cas de cellule rouge, ne pas utiliser la valeur affichée pour un dimensionnement.
---
Données produit
Gamme couverte
Famille	Modèles AC	Modèles EC
T3	VT 3311 M à VT 3423 M	VT 3311 EC à VT 3423 EC
T4	VT 4422 M à VT 4503 M	VT 4422 EC à VT 4503 EC
T5	VT 5502 M à VT 5553 M	VT 5502 EC à VT 5553 EC
T6	VT 6552 M à VT 6633 M	VT 6552 EC à VT 6633 EC
T7	VT 7712 T à VT 7713 T	VT 7712 EC à VT 7713 EC
Niveaux sonores
Les valeurs de niveau sonore sont issues des mesures YAHTEC en conditions normalisées :
Mesure en chambre anéchoïque
Distance de référence : 5 m en montage mural
Atténuation standard appliquée par le constructeur
Les niveaux réels en installation peuvent différer en fonction de la réverbération du local, de la position de montage, et des obstacles acoustiques.
---
Avertissements spécifiques
Fluides glycolés
La correction de puissance pour les fluides glycolés est basée sur des facteurs de correction globaux (Cp, ρ). Pour des concentrations élevées (> 40%) ou des températures de fonctionnement basses (< 20°C), il est recommandé de vérifier les propriétés réelles du fluide auprès du fournisseur.
Attention : L'outil ne vérifie pas que la température de fonctionnement est supérieure au point de gel du fluide. C'est à l'utilisateur de s'en assurer.
Moteur EC — tensions de commande
Les débits d'air aux différentes tensions (2V à 10V) sont issus de mesures Weiguang effectuées batterie montée. Les débits en air libre sont supérieurs — ne pas utiliser les valeurs catalogue ventilateur seul.
Altitude
La correction d'altitude affecte la densité de l'air et donc la puissance thermique côté air. Pour des altitudes supérieures à 1 000 m, l'impact devient significatif (> 8%) et doit être pris en compte dans le dimensionnement final.
---
Utilisation des résultats
Ce que vous pouvez faire avec ces résultats
✅ Réaliser une présélection de modèles pour répondre à un besoin estimé  
✅ Comparer rapidement plusieurs configurations (débit, température, fluide)  
✅ Produire un document de travail préliminaire à soumettre à un bureau d'études  
✅ Vérifier la cohérence d'un dimensionnement réalisé par ailleurs
Ce que vous ne devez pas faire
❌ Utiliser ces résultats comme spécification contractuelle  
❌ Commander du matériel sans validation d'un ingénieur thermicien  
❌ Utiliser les valeurs en dehors des plages de validité indiquées  
❌ Ignorer les cellules en rouge (régime laminaire)  
❌ Appliquer les résultats à des configurations non standard (batteries en cascade, soufflage sous faux-plancher, etc.)
---
Recommandation pour les projets
Pour tout projet, VENTIS recommande de suivre la procédure suivante :
Prédétermination avec cet outil — sélection du modèle et de la puissance approchée
Validation par un bureau d'études thermiques — calcul des besoins réels du bâtiment, vérification du dimensionnement, conformité RE2020/DTU
Consultation technique auprès de VENTIS ou de votre distributeur — confirmation du choix produit, vérification de la compatibilité avec le réseau hydraulique
Commande — sur la base du dossier technique validé
---
Informations techniques et support
Pour toute question technique sur les produits VENTIS, contactez votre interlocuteur commercial ou le service technique VENTIS.
Ce logiciel est fourni à titre gratuit, sans garantie d'aucune sorte, expresse ou implicite.
---
Calcul VENTIS v2.3-HT — Calé YAHTEC 90/70°C  
Gamme aérothermes eau chaude — Moteurs AC 2 vitesses & EC 0-10V  
© VENTIS — Document à usage interne et commercial préliminaire
