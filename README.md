# Menus de la semaine

Petite appli web pour planifier les repas de la semaine et générer la liste de courses.

## Fonctionnalités

- Tirage aléatoire des menus à partir d'une bibliothèque de plats (soirs, midis du week-end, midis en semaine en option)
- Auteur de chaque recette (David, Alex) : prénom choisi par appareil, appliqué aux ajouts et imports, filtre de la bibliothèque
- Catégories (soupes, gratins, plats en sauce, plats froids…) : classement automatique, filtre de la bibliothèque, recherche, modifiables dans la fiche
- Plats favoris (tirés 3 fois plus souvent) ou à éviter (jamais tirés automatiquement)
- Équilibre : nombre minimum de repas poisson et végé par semaine, temps maximum les soirs d'école
- Saisons : plats d'été (avril à septembre) ou d'hiver
- Restes : un plat « grande quantité » le soir est reprévu le lendemain midi (quantités doublées dans la liste)
- Cadenas pour garder un repas, relance d'un seul repas
- Crayon pour choisir un repas à la main (plat de la bibliothèque, repas libre comme « Restes », ou pas de repas)
- Vacances scolaires zone C (Paris) et jours fériés : midis à la maison automatiquement, badge sur les jours concernés (dates jusqu'à l'été 2028)
- Option mercredi midi à la maison
- Thème jour, nuit ou automatique (réglé par appareil)
- Nombre réglable de menus de la semaine précédente autorisés à ressortir
- Option pour éviter deux repas du même type (viande, poisson, végé) d'affilée
- Calendrier avec numéros de semaine ISO, chaque semaine garde son planning
- Fiche recette au clic sur un plat : ingrédients pour le foyer, étapes, temps, lien ; recette modifiable
- Placard : ingrédients déjà à la maison retirés de la liste
- Articles hors menus ajoutés à la main, et courses de chaque semaine (petit-déjeuner, goûters…)
- Produits Monoprix : produit, prix et lien relevés le 26/11/2026 sur courses.monoprix.fr pour chaque ingrédient, lien « M » dans la liste de courses, fiche produits modifiable (partagée avec le foyer)
- Budget estimé de la semaine : prix Monoprix ou indicatifs, modifiables, coût par portion, budget visé, répartition par rayon
- Copie de la liste au format Rappels (iPhone) : une ligne par article
- Export de la bibliothèque en .ods (réimportable)
- Liste de courses regroupée par rayon, quantités adaptées au foyer (2 adultes + 2 enfants par défaut, portion enfant réglable)
- Apports nutritionnels indicatifs : kcal, protéines, glucides, lipides
- Import de plats depuis un fichier `.ods`, `.xlsx` ou `.csv`

## Utilisation

Ouvrir `index.html` dans un navigateur. Aucun serveur ni installation nécessaire.

Les données (plannings, bibliothèque, réglages) sont enregistrées dans le navigateur (`localStorage`).

## Partage du foyer

Depuis https://plutus2811.github.io/menus/, la section « Partage du foyer » synchronise en direct le planning, la bibliothèque et la liste de courses entre plusieurs appareils, via Firebase Firestore.

1. Sur un appareil : « Créer un foyer », puis « Copier le lien d'invitation ».
2. Ouvrir ce lien sur les autres appareils : ils rejoignent le foyer automatiquement.

Règles Firestore utilisées (un foyer n'est accessible qu'avec son code de 24 caractères) :

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /foyers/{foyer} {
      allow read, write: if foyer.size() >= 20;
    }
  }
}
```

La clé `apiKey` Firebase présente dans `index.html` est un identifiant public prévu pour être dans le code d'un site ; la protection des données repose sur les règles ci-dessus.

## Format d'import

Une ligne par ingrédient, quantités pour 1 adulte. Laisser « Plat » vide pour continuer le plat du dessus. Les colonnes nutritionnelles (pour 100 g) sont facultatives, ainsi que Préparation (min), Cuisson (min), Lien, Étapes (séparées par « ; »), Saison (été / hiver), Favori (oui / éviter), Restes (oui), Auteur et Catégories (séparées par des virgules), sur la ligne du plat.

| Plat | Type | Quantité | Unité | Ingrédient | Rayon | kcal | Protéines | Glucides | Lipides | g/pièce |
|---|---|---|---|---|---|---|---|---|---|---|
| Lasagnes | viande | 100 | g | bœuf haché | Boucherie | | | | | |
| | | 3 | pièce | feuilles de lasagne | Épicerie | 350 | 12 | 70 | 1.5 | 20 |

Les valeurs nutritionnelles fournies sont des ordres de grandeur, pas des données de référence.
