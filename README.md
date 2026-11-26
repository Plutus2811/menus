# Menus de la semaine

Petite appli web pour planifier les repas de la semaine et générer la liste de courses.

## Fonctionnalités

- Tirage aléatoire des menus à partir d'une bibliothèque de plats (soirs, midis du week-end, midis en semaine en option)
- Cadenas pour garder un repas, relance d'un seul repas
- Nombre réglable de menus de la semaine précédente autorisés à ressortir
- Option pour éviter deux repas du même type (viande, poisson, végé) d'affilée
- Calendrier avec numéros de semaine ISO, chaque semaine garde son planning
- Liste de courses regroupée par rayon, quantités adaptées au foyer (2 adultes + 2 enfants par défaut, portion enfant réglable)
- Apports nutritionnels indicatifs : kcal, protéines, glucides, lipides
- Import de plats depuis un fichier `.ods`, `.xlsx` ou `.csv`

## Utilisation

Ouvrir `index.html` dans un navigateur. Aucun serveur ni installation nécessaire.

Les données (plannings, bibliothèque, réglages) sont enregistrées dans le navigateur (`localStorage`) : elles ne sont pas partagées entre appareils.

## Format d'import

Une ligne par ingrédient, quantités pour 1 adulte. Laisser « Plat » vide pour continuer le plat du dessus. Les colonnes nutritionnelles (pour 100 g) sont facultatives.

| Plat | Type | Quantité | Unité | Ingrédient | Rayon | kcal | Protéines | Glucides | Lipides | g/pièce |
|---|---|---|---|---|---|---|---|---|---|---|
| Lasagnes | viande | 100 | g | bœuf haché | Boucherie | | | | | |
| | | 3 | pièce | feuilles de lasagne | Épicerie | 350 | 12 | 70 | 1.5 | 20 |

Les valeurs nutritionnelles fournies sont des ordres de grandeur, pas des données de référence.
