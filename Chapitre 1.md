# Chapitre 1 : Rappel du langage R

- [Chapitre 1 : Rappel du langage R](#chapitre-1--rappel-du-langage-r)
  - [Objectifs](#objectifs)
  - [Importation des données :](#importation-des-données-)
  - [Statistiques générales](#statistiques-générales)
  - [Manipulation des données :](#manipulation-des-données-)
    - [Découvrir le package `dplyr`](#découvrir-le-package-dplyr)
    - [Filtre](#filtre)
    - [Agrégation](#agrégation)
  - [Création de graphique  :](#création-de-graphique--)
    - [Graphiques élémentaires](#graphiques-élémentaires)
    - [Régression linéaire simple](#régression-linéaire-simple)
    - [Cartographie](#cartographie)
  - [Liens utiles](#liens-utiles)

## Objectifs

Voici les objectifs de ce chapitre :
- [x] Rappel des bases du langage
- [x] Manipuler des vecteurs
- [x] Manipuler des dataframes
- [x] Calculer des statistiques
- [x] Construire des graphiques

Avec l’accélération du changement climatique et la hausse des prix de l’énergie, la sobriété énergétique est au cœur des préoccupations des Français. Aussi, afin d’éclairer et inspirer les acteurs de la transition écologique, Enedis propose des analyses et chiffres clés pour éclairer et orienter les décisions.

Dans ce contexte, le Diagnostic de Performance Energétique (DPE) permet d’évaluer la performance énergétique et climatique d’un bâtiment. Il consiste en une étiquette pouvant aller de A à G pour chaque logement ou bâtiment, qui évalue sa consommation d’énergie et son impact en terme d’émission de GES. Il sert notamment à identifier les passoires énergétiques (étiquettes F et G du DPE, c’est-à-dire les logements qui consomment le plus d’énergie et/ou émettent le plus de gaz à effet de serre). Il a pour objectif d’informer l’acquéreur ou le locataire sur la « valeur verte », de recommander des travaux à réaliser pour l’améliorer et d’estimer ses charges énergétiques. De plus, la mise en location de ces passoires thermiques sera progressivement interdite (interdiction pour les bâtiments notés G+ au 1er janvier 2023, qui sera étendue par la suite).

Les données ne seront pas représentatives de la France et ne peuvent donc pas être agrégées à la maille de la France entière. On suppose néanmoins que les données pourront permettre de donner déjà des informations intéressantes bien que non exhaustives. Dans ce chapitre, nous travaillerons sur un échantillon basé sur des logements du 8ème arrondissement de Lyon.

## Importation des données : 

1. Télécharger les jeux de données `dpe-v2-logements-existants.csv` et `dpe-v2-logements-neufs.csv` disponibles [ici](./data).
2. Importer les jeux de données
3. Afficher la dimension des 2 datasets
4. Créer une colonne nommée `Logement` dans les deux datasets avec la valeur `ancien` ou `neuf` selon la source.
5. Fusionner les deux dataframes avec uniquement les colonnes communes. Plus d'info dans le [dictionnaire de données](https://data.ademe.fr/data-fair/api/v1/datasets/dpe-v2-logements-existants/metadata-attachments/DPE_Dictionnaire%20de%20donn%C3%A9es_JDD_V3.pdf).
6. Créer une colonne avec uniquement l'année de la `Date de réception du DPE`
7. Créer une colonne qui vérifie si `Coût_total_5_usages` correspond bien à la somme du `Coût_chauffage` + `Coût_éclairage` + `Coût_ECS` + `Coût_refroidissement` +  `Coût_auxiliaires`.
8. Créer une colonne `Coût chaufage en %` qui est la part du coût du chauffage dans le coût total 5 usages.

## Statistiques générales

1. Calculer le nombre de DPE par Etiquette DPE
2. Calculer le nombre de DPE par année
3. Calculer le nombre de DPE par type logement (ancien/neuf)
4. Calculer la nombre de DPE par type de Bâtiment
5. Calculer la nombre de DPE par type d'installation chauffage en pourcentage
6. Calculer la nombre de DPE par période de construction
7. Calculer la surface habitable moyenne des logements
8. Calculer la moyenne du coût_chauffage
9. Calculer les quartiles puis déciles du Coût_ECS
10. Calculer le coefficient de corrélation entre la surface habitable du logement et le coût du chauffage.
11. Construire un corrélogramme sur ces variables (`Coût_total_5_usages`,`Coût_chauffage`,`Coût_éclairage`,`Coût_ECS`,`Coût_refroidissement`, `Coût_auxiliaires`, `Surface_habitable_logement` , `Emission_GES_5_usages`)

## Manipulation des données : 

### Découvrir le package `dplyr`

Pour cet exercice suivre [ce cours](https://asardell.github.io/programmation-r/dplyr.html#dplyr) avant de répondre aux questions suivantes : 

| Nom de la commande | Description | Arguments Pertinents | Exemple |
|--------------------|-------------|----------------------|---------|
| `select()` | Sélectionne des colonnes d'un jeu de données. | `data` : le jeu de données, `...` : les colonnes à sélectionner | `dplyr::select(data = dataframe, col1, col2)` |
| `slice()` | Sélectionne des lignes spécifiques d'un jeu de données. | `data` : le jeu de données, `rows` : les rangs à sélectionner | `dplyr::slice(data = dataframe, rows = c(1, 3, 5))` |
| `filter()` | Filtre les lignes d'un jeu de données en fonction de conditions spécifiques. | `data` : le jeu de données, `...` : les conditions de filtrage | `dplyr::filter(data = dataframe, col1 > 10)` |
| `arrange()` | Trie les lignes d'un jeu de données en fonction de variables spécifiques. | `data` : le jeu de données, `...` : les variables de tri | `dplyr::arrange(data = dataframe, col1)` |
| `group_by()` | Crée des groupes de données en fonction de variables spécifiques. | `data` : le jeu de données, `...` : les variables de groupe | `dplyr::group_by(data = dataframe, col1)` |
| `summarise()` | Résume les données groupées en effectuant des calculs. | `data` : le jeu de données, `...` : les calculs à effectuer | `dplyr::summarise(data = dataframe, mean_col1 = mean(col1))` |

### Filtre

1. Créer un dataframe avec uniquement les logements dont le type de batîment est un appartement
2. Créer un dataframe avec uniquement les logements dont l'étiquette DPE est D,E,F,G
3. Créer un dataframe avec les logements anciens dont la période de construction est *avant 1948*
4. Créer un dataframe avec les logements qui ont une surface habitable strictement supérieure à la surface habitable moyenne
5. Créer un dataframe en triant les logements qui consomme le plus d'énergie 5 usages en m² à ceux qui consomme le moins
6. Créer un dataframe en triant par étiquette DPE, puis période de construction, puis par coût en chauffage décroissant.

### Agrégation

1. Calculer le coût moyen du chauffage  selon l'étiquette du DPE
2. Calculer la moyenne de la consommation annuelle  5 usages en energie en kWhef/an selon la période de construction
3. Calculer la moyenne de la consommation annuelle  5 usages en energie en kWhef/an selon le type de logement et d'étiquette DPE

## Création de graphique  : 

### Graphiques élémentaires 

1. Construire une histogramme de la distribution des surfaces habitables
2. Construire un boxplot de la distribution du la onsommation annuelle  5 usages en energie en kWhef/an
3. Construire un boxplot avec le coût du chauffage selon le type d'étiquette DPE
4. Construire un diagramme en barre du nombre de logements par période de construction
5. Construire un diagramme circulaire du principal type d'énergie (`Type_énergie_n.1`)

### Régression linéaire simple

1. Construire une nuage de point entre la surface habitable du logement et le coût du chauffage
2. Calculer le coefficient de corrélation entre la surface habitable du logement et le coût du chauffage.
3. Construire une régression linéaire simple pour modéliser le coût du chauffage en fonction de la surface habitable
4. Analyser les coefficients de la régression
5. Affichier la droite de régression sur le nuage de point

### Cartographie

1. Télécharger le jeu de données `adresses-69` disponibles [ici](./data).
2. Importer le jeu de données
3. Réaliser une jointure sur le champ `Identifiant__BAN` pour ajouter les coordonnées GPS (lattitude / longitude) au dataframe initial
4. Construire une carte simple à partir de [l'exemple de SD1](https://github.com/asardell/IUT_SD1/blob/main/TD4.md#exercice-6---cartographie-spoil-sur-le-sd2)
5. Construire une carte personnalisée à partir en parcourant ce [tutoriel](https://rstudio.github.io/leaflet/articles/markers.html)


## Liens utiles

Voici quelques liens utiles :

- [Cours de SD1](https://github.com/asardell/IUT_SD1)
- [Cours sur la programmation R](https://asardell.github.io/programmation-r/)
- [Contexte du Challenge ENEDIS](https://defis.data.gouv.fr/defis/65b76f15d7874915c8e41298)
- [Base Adresse Nationale](https://adresse.data.gouv.fr/donnees-nationales)
- [Comprendre son DPE](https://www.ecologie.gouv.fr/sites/default/files/documents/comprendre_mon_dpe.pdf)
- [Dictionnaire de données](https://data.ademe.fr/data-fair/api/v1/datasets/dpe-v2-logements-existants/metadata-attachments/DPE_Dictionnaire%20de%20donn%C3%A9es_JDD_V3.pdf)
- [Carte interactive avec leaflet](https://rstudio.github.io/leaflet/articles/markers.html)