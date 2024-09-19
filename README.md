# IUT_SD2

Ce document `README.md` est présent dans tous les repositories GitHub. Il permet de présenter le contenu du référentiel Git.
Ce documet est écrit dans le cadre du module de programmation statistiques sous R.

## Objectifs globaux

Voici les objectifs de ce module :
- [x] Rappels du langage R
- [x] Initiation au R Markdown pour  développer des rapports statistiques automatisé
- [x] Initiation au R Shiny pour développer des applications intéractives
- [x] Bonne pratique et usage de Git pour documenter, versionner et collaborer dans un projet de développement

## Planning

1. Chapitre 1 : Rappel du langage R
2. Chapitre 2 : Utiliser une API pour extraire des données
3. Chapitre 3 : Initiation à Git avec GitHub Desktop
4. Chapitre 4 : Initiation au R Markdown
5. Chapitre 5 : [Initiation au R Shiny](https://shiny.posit.co/r/getstarted/shiny-basics/lesson1/index.html)

## Liens utiles

Voici quelques liens utiles :

- [Markdown Cheat Sheet](https://www.markdownguide.org/cheat-sheet/)
- [GitHub Cheat Sheet](https://training.github.com/downloads/fr/github-git-cheat-sheet.pdf)
- [GitHub Get Started](https://docs.github.com/fr/get-started/quickstart/hello-world)
- [GitHub Set up](https://docs.github.com/fr/get-started/quickstart/set-up-git)
- [Cours de SD1](https://github.com/asardell/IUT_SD1)
- [Cours sur la programmation R](https://asardell.github.io/programmation-r/)

## Tableau Récap

### Syntaxe des commandes élémentaires

| Nom de la commande | Description | Argument Pertinent | Exemple |
|------------------|-------------|--------------------|---------|
| `$` | Accéder à une colonne d'un dataframe | | `df$colonneA` |
| `[ , ]` | Accéder à certaines lignes et/ou colonnes d'un datarame. | | `dfExtraction <- df[ c(5,6), c("colonneB", "colonneD")]` |
| `[ ]` | Accéder aux éléments d'un vecteur. | | `vecteur1[4]` |
| `:` | Génère un séquence avec un pas de 1. | | `sequence <- 8:15` |
| `[-1]` | Accèder à tous les éléments sauf ceux précisés. | | `vecteur1[-4]` |
| `[ , ]` | Indexe un dataframe au niveau des lignes et des colonnes. | `row_index` : index ou condition pour sélectionner les lignes, `col_index` : index ou noms de colonnes pour sélectionner les colonnes. | `donnees_subset <- donnees[1:10, c("colonne1", "colonne2")]` |
| `[ - , ]` | Indexation inverse, exclut les lignes ou colonnes spécifiées. | `row_index` : index ou condition pour exclure les lignes, `col_index` : index ou noms de colonnes pour exclure les colonnes. | `donnees_sans_colonne3 <- donnees[, -3]` |

### Syntaxe des opérateurs logiques

| Opérateur logique | Description | Exemple avec la fonction `subset()` |
|-------------------|-------------|----------------------------------------|
| `>` | Vérifie si une valeur est strictement supérieure à une autre. | `subset(dataframe, colonne1 > 10)` |
| `>=` | Vérifie si une valeur est supérieure ou égale à une autre. | `subset(dataframe, colonne2 >= 0)` |
| `<` | Vérifie si une valeur est strictement inférieure à une autre. | `subset(dataframe, colonne3 < 5)` |
| `<=` | Vérifie si une valeur est inférieure ou égale à une autre. | `subset(dataframe, colonne4 <= 100)` |
| `&` | Opérateur logique ET, renvoie TRUE si les deux conditions sont remplies. | `subset(dataframe, colonne1 > 10 & colonne2 < 5)` |
| `\|` | Opérateur logique OU, renvoie TRUE si au moins l'une des conditions est remplie. | `subset(dataframe, colonne3 == "oui" \| colonne4 != "non")` |
| `!=` | Vérifie si deux valeurs sont différentes. | `subset(dataframe, colonne5 != "invalide")` |
| `==` | Vérifie si deux valeurs sont égales. | `subset(dataframe, colonne6 == "valide")` |
| `%in%` | Vérifie si une valeur est présente dans un vecteur ou une liste. | `subset(dataframe, colonne7 %in% c("valeur1", "valeur2", "valeur3"))` |
| `!` | Opérateur logique NON, renvoie l'inverse d'une condition. | `subset(dataframe, !colonne8 %in% c("B","C"))` |

### Syntaxe des fonctionnalités utiles

| Nom de la fonction | Description | Argument Pertinent | Exemple |
|------------------|-------------|--------------------|---------|
| `c()` | Concatène des vecteurs ou des valeurs pour créer un nouveau vecteur. |  | `nouveaux_vecteur <- c(vecteur1, vecteur2)` |
| `rm()` | Supprime des objets (variables ou fonctions) de l'environnement. | `list = ls()` supprime tous les objets | `rm(objet1, objet2)` |
| `print()` | Affiche dans la console. | | `print(objet1)` |
| `seq()` | Génère une séquence de nombres. | `from`, `to`, `by` spécifiant le début, la fin et l'incrément. | `sequence <- seq(1, 10, by = 2)` |
| `rep()` | Répète les éléments d'un vecteur plusieurs fois. | `times` spécifiant le nombre de répétitions. | `replication <- rep(5, times = 5)` |
| `length()` | Retourne la longueur d'un vecteur. |  | `longueur <- length(vecteur)` |
| `class()` | Retourne le type de classe d'un objet. |  | `type_classe <- class(objet)` |
| `sum()` | Calcule la somme des éléments d'un vecteur. | `na.rm` : spécifie si les valeurs NA doivent être retirées (par défaut FALSE). | `somme <- sum(vecteur)` |
| `mean()` | Calcule la moyenne des éléments d'un vecteur. | `na.rm` : spécifie si les valeurs NA doivent être retirées (par défaut FALSE). | `moyenne <- mean(vecteur)` |
| `median()` | Calcule la médiane d'un vecteur. | `na.rm` : spécifie si les valeurs NA doivent être retirées (par défaut FALSE). | `mediane <- median(vecteur)` |
| `min()` | Retourne la valeur minimale d'un vecteur. | `na.rm` : spécifie si les valeurs NA doivent être retirées (par défaut FALSE).  | `minimum <- min(vecteur)` |
| `max()` | Retourne la valeur maximale d'un vecteur. | `na.rm` : spécifie si les valeurs NA doivent être retirées (par défaut FALSE).  | `maximum <- max(vecteur)` |
| `sd()` | Calcule l'écart type d'un vecteur. | `na.rm` : spécifie si les valeurs NA doivent être retirées (par défaut FALSE).  | `ecart_type <- sd(vecteur)` |
| `var()` | Calcule la variance d'un vecteur. | `na.rm` : spécifie si les valeurs NA doivent être retirées (par défaut FALSE).  | `variance <- var(vecteur)` |
| `quantile()` | Calcule les quantiles d'un vecteur. | `x` : le vecteur pour lequel calculer les quantiles. `probs` : les quantiles à calculer (par exemple, c(0.25, 0.5, 0.75)). `na.rm` : spécifie si les valeurs NA doivent être retirées (par défaut FALSE). | `quantiles <- quantile(vecteur, probs = c(0.25, 0.5, 0.75))` |
| `sort()` | Trie les éléments d'un vecteur ou d'une matrice. | `x` : le vecteur ou la matrice à trier. `decreasing` : un booléen indiquant si le tri doit être effectué par ordre décroissant (par défaut, `FALSE`). | `vecteur_tri <- sort(vecteur)` |
| `unique()` | Retourne les valeurs uniques d'un vecteur. |  | `valeurs_uniques <- unique(vecteur)` |
| `round()` | Arrondit les nombres d'un vecteur à un nombre spécifié de décimales. | `x` : le vecteur à arrondir. `digits` : nombre de décimales (par défaut 0). | `arrondi <- round(3.14159, digits = 2)` |
| `abs()` | Calcule la valeur absolue des éléments d'un vecteur. | | `valeurs_absolues <- abs(vecteur)` |
| `table()` | Construit une table de fréquences pour un vecteur ou une combinaison de vecteurs. | `x` : vecteur ou combinaison de vecteurs pour lesquels construire la table. | `table_frequences <- table(vecteur)` |
| `prop.table()` | Convertit les fréquences d'une table en proportions. | `x` : la table de fréquences à convertir. `margin` : indique les marges à utiliser lors du calcul des proportions (par défaut, `NULL` signifie utiliser toutes les marges). | `proportions <- prop.table(table_frequences)` |
| `rnorm()` | Génère des échantillons aléatoires suivant une distribution normale. | `n` : nombre d'échantillons à générer. `mean` : moyenne de la distribution. `sd` : écart-type de la distribution. | `echantillon_norm <- rnorm(100, mean = 10, sd = 2)` |
| `runif()` | Génère des échantillons aléatoires suivant une distribution uniforme. | `n` : nombre d'échantillons à générer. `min` : valeur minimale de la distribution. `max` : valeur maximale de la distribution. | `echantillon_unif <- runif(50, min = 0, max = 1)` |
| `sample()` | Sélectionne un échantillon aléatoire à partir d'un vecteur. | `x` : vecteur à partir duquel échantillonner. `size` : taille de l'échantillon. `replace` : avec ou sans remise.| `echantillon_aleatoire <- sample(vecteur, size = 3, replace = TRUE)` |
| `hist()` | Crée un histogramme à partir d'un vecteur de données. | `x` : le vecteur de données à utiliser. `breaks` : le nombre de bâtons (barres) dans l'histogramme. | `histogramme <- hist(data_vector, breaks = 10)` |
| `boxplot()` | Crée une boîte à moustaches à partir d'un ou plusieurs vecteurs de données. | `x` : un ou plusieurs vecteurs de données à utiliser. | `boite_moustaches <- boxplot(data_vector1, data_vector2)` |
| `data()` | Retourne la liste des noms des jeux de données chargés par défaut. |  | `data()` |
| `ncol()` | Retourne le nombre de colonnes dans un objet (par exemple, un dataframe ou une matrice). |  | `nombre_colonnes <- ncol(objet)` |
| `nrow()` | Retourne le nombre de lignes dans un objet (par exemple, un dataframe ou une matrice). |  | `nombre_lignes <- nrow(objet)` |
| `dim()` | Retourne les dimensions (nombre de lignes et de colonnes) d'un objet (par exemple, un dataframe ou une matrice). |  | `dimensions <- dim(objet)` |
| `colnames()` | Retourne ou définie les noms des colonnes dans un dataframe ou une matrice. | Aucun ou nouveaux noms de colonnes | `noms_colonnes <- colnames(dataframe)` ou `colnames(dataframe) <- c("Nom1", "Nom2", ...)` |
| `summary()` | Produit un résumé statistique des données dans un objet (par exemple, un vecteur, un dataframe, etc.). |  | `res <- summary(objet)` |
| `View()` | Ouvre une visionneuse de données pour explorer un dataframe ou une matrice dans une fenêtre séparée. | Aucun | `View(dataframe)` |
| `head()` | Affiche les premières lignes d'un dataframe ou d'une matrice. | `n` : nombre de lignes à afficher (par défaut 6) | `premieres_lignes <- head(dataframe, n = 10)` |
| `read.csv()` | Lit un fichier CSV et retourne un dataframe. | `file` : le chemin ou l'URL du fichier CSV à lire, `header` : spécifie si la première ligne contient les noms des variables (par défaut TRUE), `dec` : le caractère utilisé pour indiquer le point décimal (par défaut "."), `sep` : le séparateur de champ (par défaut ","). | `donnees <- read.csv("fichier.csv", header = TRUE, dec = ",", sep = ";")` |
| `subset()` | Retourne un sous-ensemble d'un objet (par exemple, un dataframe) en fonction de certaines conditions. | `x` : l'objet à sous-ensemble, `subset` : la condition de sous-ensemble. | `sous_ensemble <- subset(dataframe, condition)` |
| `write.table()` | Écrit un objet (par exemple, un dataframe) dans un fichier texte ou CSV. | `x` : l'objet à écrire, `file` : le nom du fichier de sortie, `sep` : le séparateur de champ (par défaut " "), `row.names` : spécifie si les noms de lignes doivent être inclus (par défaut TRUE). | `write.table(dataframe, file = "output.csv", sep = ",", row.names = FALSE)` |
| `rbind()` | Ajoute des lignes à un dataframe existant en les liant par les colonnes. | `nouveau_dataframe <- rbind(dataframe1, dataframe2)` |
| `getwd()` | Retourne le répertoire de travail actuel. | | `current_dir <- getwd()` |
| `setwd()` | Change le répertoire de travail actuel. | `dir` : le chemin du nouveau répertoire de travail | `setwd("/chemin/vers/le/nouveau/repertoire")` |
| `cor()` | Calcule la corrélation entre deux vecteurs. | `x` : le premier vecteur, `y` : le deuxième vecteur, `method` : la méthode de calcul de la corrélation (par défaut "pearson"). | `correlation <- cor(x = vecteur1, y = vecteur2, method = "spearman")` |
| `plot()` | Trace un nuage de points entre deux vecteurs. | `x` : le premier vecteur, `y` : le deuxième vecteur, `xlab` : étiquette de l'axe des abscisses, `ylab` : étiquette de l'axe des ordonnées, `main` : titre du graphique. | `plot(vecteur1, vecteur2, xlab = "Variable X", ylab = "Variable Y", main = "Nuage de points")` |
| `cov()` | Calcule la covariance entre deux vecteurs. | `x` : le premier vecteur, `y` : le deuxième vecteur. | `covariance <- cov(x = vecteur1, y = vecteur2)` |
| `install.packages()` | Installe un package R depuis un dépôt CRAN ou local. | `pkgs` : le nom du package à installer, `repos` : l'URL du dépôt, `dependencies` : spécifie si les dépendances doivent également être installées (par défaut TRUE). | `install.packages("nom_du_package")` |
| `library()` | Charge un package R déjà installé en mémoire pour être utilisé dans la session R courante. | `package` : le nom du package à charger. | `library(nom_du_package)` |
| `order()` | Trie les éléments d'un vecteur et retourne les indices dans l'ordre croissant ou décroissant. | `x` : le vecteur à trier, `decreasing` : spécifie si le tri doit être effectué dans l'ordre décroissant (par défaut FALSE). | `indices_tri <- order(vecteur, decreasing = FALSE)` |
| `read_excel()` | Lit un fichier Excel dans R. | `path` : le chemin vers le fichier Excel, `sheet` : le nom ou l'index de la feuille à lire | `readxl::read_excel(path = "/chemin/vers/votre/fichier.xlsx", sheet = "Nom_de_la_feuille")` |
| `as.factor()` | Convertit un vecteur en facteur. | `x` : le vecteur à convertir | `as.factor(x = c("A", "B", "A", "C"))` |
| `ifelse()` | Retourne des valeurs en fonction d'une condition. | `test` : la condition logique à évaluer, `yes` : la valeur à retourner si la condition est vraie, `no` : la valeur à retourner si la condition est fausse | `ifelse(test = x > 0, yes = "Positif", no = "Négatif")` |
| `cut()` | Divise les valeurs numériques en intervalles. | `x` : le vecteur de valeurs numériques à découper, `breaks` : les points de rupture pour diviser les valeurs, `labels` : les étiquettes à attribuer aux intervalles | `cut(x = c(1, 2, 3, 4, 5), breaks = 3, labels = c("Faible", "Moyen", "Fort"))` |
| `is.na()` | Vérifie si les valeurs sont manquantes (NA). | `x` : le vecteur à tester | `is.na(x)` |
| `aggregate()` | Effectue une opération d'agrégation sur les données groupées. | `x` : formule spécifiant les variables à agréger et les variables de groupe, `data` : le jeu de données, `FUN` :  la ou les fonctions d'agrégation souhaitées | `aggregate(x = y ~ a + b, data = dataframe, FUN = function(x) mean(x))` |
| `points()` | Ajoute des points à un graphique existant. | `x`, `y` : les coordonnées des points <br> `...` : autres arguments pour personnaliser les points | `points(x = data$x, y = data$y, col = "red")` |
| `lines()` | Ajoute des lignes à un graphique existant. | `x`, `y` : les coordonnées des points pour les lignes <br> `...` : autres arguments pour personnaliser les lignes | `lines(x = data$x, y = data$y, col = "blue")` |
| `abline()` | Ajoute une ligne à un graphique existant. | `a`, `b` : paramètres de la ligne <br> `h`, `v` : positions pour les lignes horizontales ou verticales <br> `...` : autres arguments pour personnaliser la ligne | `abline(a = 0, b = 1, col = "red", lty = 2)` |
| `legend()` | Ajoute une légende à un graphique. | `x`, `y` : les coordonnées de la légende <br> `legend` : les labels de la légende <br> `fill`, `col` : les couleurs des éléments de la légende <br> `title` : le titre de la légende | `legend(x = "topright", y = "bottomleft", legend = c("Groupe 1", "Groupe 2"), fill = c("red", "blue"), title = "Groupes")` |
| `barplot()` | Crée un diagramme à barres. | `height` : les hauteurs des barres <br> `names.arg` : les étiquettes des barres <br> `main` : le titre du graphique <br> `xlab` : le label de l'axe des abscisses <br> `ylab` : le label de l'axe des ordonnées <br> `col` : la couleur des barres | `barplot(height = c(1, 2, 3), names.arg = c("A", "B", "C"), main = "Diagramme à barres", xlab = "Groupes", ylab = "Fréquence", col = "blue")` |
| `pie()` | Crée un diagramme circulaire. | `x` : les proportions à représenter <br> `labels` : les étiquettes des sections <br> `main` : le titre du graphique <br> `col` : les couleurs des sections | `pie(x = c(0.2, 0.3, 0.5), labels = c("A", "B", "C"), main = "Diagramme circulaire", col = c("red", "green", "blue"))` |
| `boxplot()` | Crée une boîte à moustaches. | `formula` : la formule indiquant les variables à utiliser <br> `data` : le jeu de données <br> `main` : le titre du graphique <br> `col` : la couleur des boîtes | `boxplot(formula = y ~ group, data = df, main = "Boîte à moustaches", col = "blue")` |
| `plot()` | Crée un nuage de points ou un autre type de graphique. | `x`, `y` : les données à tracer <br> `main` : le titre du graphique <br> `xlab` : le label de l'axe des abscisses <br> `ylab` : le label de l'axe des ordonnées <br> `col` : la couleur des points ou des lignes | `plot(x = df$variable1, y = df$variable2, main = "Nuage de points", xlab = "Variable X", ylab = "Variable Y", col = "blue")` |
| `hist()` | Crée un histogramme à partir des données. | `x` : les données à utiliser <br> `main` : le titre du graphique <br> `xlab` : le label de l'axe des abscisses <br> `ylab` : le label de l'axe des ordonnées <br> `col` : la couleur des barres | `hist(x = df$variable, main = "Histogramme", xlab = "Variable", ylab = "Fréquence", col = "blue")` |
| `par()` | Modifie les paramètres graphiques de base. | `mfrow` : spécifie le nombre de lignes et de colonnes dans la fenêtre de graphique | `par(mfrow = c(2, 2))` |
| `is.numeric()` | Vérifie si un objet est de type numérique. | `x` : l'objet à vérifier | `is.numeric(x)` |
| `function(toto, tata = valeur_par_defaut) { ... }` | Définit une fonction avec un argument obligatoire et un argument facultatif avec une valeur par défaut. | `toto` : l'argument requis pour la fonction<br> `tata` : l'argument qui peut être omis lors de l'appel de la fonction, avec une valeur par défaut | `my_function <- function(toto, tata = 1) { ... }` |
| `return(objet_a_retourner)` | Termine l'exécution d'une fonction et renvoie une valeur spécifiée. | `objet_a_retourner` : la valeur à renvoyer à partir de la fonction | `return(resultat)` |
| `if(condition) { bloc_de_code }` | Exécute un bloc de code si la condition est vraie. | `condition` : la condition à évaluer | `if(x > 0) { print("x est positif") }` |
| `if(condition) { bloc_de_code } else { autre_bloc_de_code }` | Exécute un bloc de code si la condition est vraie, sinon exécute un autre bloc de code. | `condition` : la condition à évaluer | `if(x > 0) { print("x est positif") } else { print("x est négatif ou nul") }` |
| `if(condition1) { bloc_de_code1 } else if(condition2) { bloc_de_code2 }` | Exécute un bloc de code si la première condition est vraie, sinon vérifie une autre condition et exécute un autre bloc de code si cette condition est vraie. | `condition1`, `condition2` : les conditions à évaluer | `if(x > 0) { print("x est positif") } else if(x == 0) { print("x est nul") }` |
| `readline(prompt = "")` | Lit une ligne depuis l'entrée standard (généralement le clavier). | `prompt` : le message à afficher à l'utilisateur pour le guider lors de la saisie | `valeur <- readline(prompt = "Veuillez saisir une valeur : ")` |
| `cat(..., sep = " ")` | Concatène et imprime les éléments fournis. | `...` : les objets à imprimer <br> `sep` : le séparateur à utiliser entre les éléments (par défaut, un espace) | `cat("Hello", "world!", sep = " ")` |
| `for (variable in sequence) { ... }` | Exécute un bloc de code pour chaque valeur dans une séquence spécifiée. | `variable` : la variable qui prendra les valeurs de la séquence à chaque itération | `for (i in 1:10) { ... }` |
| `while (condition) { ... }` | Exécute un bloc de code tant qu'une condition spécifiée est vraie. | `condition` : l'expression logique qui doit être vraie pour continuer à exécuter le bloc de code | `while (x < 10) { ... }` |
| `list.files(path = ".", pattern = NULL, ...) ` | Renvoie une liste de noms de fichiers dans un répertoire donné. | `path` : le chemin du répertoire à examiner (par défaut, le répertoire de travail actuel) <br> `pattern` : un motif de recherche pour filtrer les noms de fichiers (par défaut, tous les fichiers) | `fichiers <- list.files(path = "chemin/vers/repertoire", pattern = "*.txt")` |
| `file.info(...)`   | Renvoie des informations sur les fichiers spécifiés. | `...` : une liste de chemins de fichiers ou de répertoires à examiner. | `info <- file.info("chemin/vers/fichier.txt")` |
| `tolower(x)`   | Convertit les caractères en minuscules. | `x` : le vecteur ou la chaîne de caractères à convertir en minuscules. | `chaine_minuscule <- tolower("Bonjour MONDE")` |
| `rnorm()` | Génère des échantillons aléatoires suivant une distribution normale $N(μ,σ)$ . | `n` : nombre d'échantillons à générer. `mean` : moyenne de la distribution. `sd` : écart-type de la distribution. | `echantillon_norm <- rnorm(100, mean = 10, sd = 2)` |
| `qnorm()` | Calcule les quantiles de la distribution normale spécifiée. | `p` : probabilité pour laquelle trouver le quantile. `mean` : moyenne de la distribution. `sd` : écart-type de la distribution. | `quantile <- qnorm(0.975, mean = 0, sd = 1)` |
| `pnorm()` | Calcule la fonction de distribution cumulative (CDF) pour la distribution normale spécifiée. | `q` : valeur pour laquelle calculer la probabilité. `mean` : moyenne de la distribution. `sd` : écart-type de la distribution. | `pnorm(q = 1.96, mean = 0, sd = 1)` |
| `cbind()` | Combine des vecteurs, des matrices ou des data frames par colonne. | `...` : une ou plusieurs objets R à combiner, tels que des vecteurs, des matrices ou des data frames. | `combined_data <- cbind(vector1, vector2, ...)` |
| `rownames()` | Renvoie ou définit les noms des lignes d'un objet R. | `x` : objet R pour lequel obtenir ou définir les noms des lignes. | `rownames(dataframe) <- new_row_names` |
| `colnames()` | Renvoie ou définit les noms des colonnes d'un objet R. | `x` : objet R pour lequel obtenir ou définir les noms des colonnes. | `colnames(dataframe) <- new_col_names` |
| `sqrt()` | Calcule la racine carrée d'un nombre ou d'un vecteur d'éléments. | `x` : nombre ou vecteur dont calculer la racine carrée. | `result <- sqrt(16)` |
| `replicate()` | Répète l'évaluation d'une expression un certain nombre de fois et retourne les résultats sous forme de vecteur, de liste ou de tableau. | `n` : nombre de répétitions. `expr` : expression à évaluer. | `result <- replicate(n = 3, expr = mean(rnorm(100)))` |
| `apply()` | Applique une fonction sur les marges d'un tableau (matrice ou data frame). | `X` : tableau (matrice ou data frame) sur lequel appliquer la fonction. `MARGIN` : spécifie les marges sur lesquelles appliquer la fonction (1 pour les lignes, 2 pour les colonnes). `FUN` : fonction à appliquer. `...` : arguments supplémentaires à passer à la fonction. | `result <- apply(X = df, MARGIN = 1, FUN = function(x) mean(x))` |
| `basename()` | Extrait le nom de fichier de chaque chemin dans un vecteur de chemins. | `path` : le chemin ou les chemins dont vous voulez extraire les noms de fichier. | `nom_fichier <- basename(fichiers[1])` |
| `file_path_sans_ext()` (package `tools`) | Extrait le nom de fichier sans extension à partir d'un chemin ou nom de fichier. | `path` : le chemin ou le nom du fichier dont vous voulez extraire le nom sans extension. | `nom_sans_ext <- file_path_sans_ext(nom_fichier)` |
| `assign()` | Affecte une valeur à un objet spécifié par un nom. | `x` : le nom de l'objet à créer ou modifier. `value` : la valeur à lui assigner. | `assign(nom_sans_ext, valeur)` |
| `Sys.time()` | Retourne l'heure système actuelle sous forme d'objet de classe `POSIXct`. | | `heure_actuelle <- Sys.time()` |
