# Chapitre 4 : Initiation au R Markdown

## Objectifs

Voici les objectifs de ce module :
- [x] Créer un Rmarkdown
- [x] Utiliser les options des Chunks
- [x] Afficher des tableaux
- [x] Utiliser des variables
- [x] Utiliser des paramètres


1. En-tête de métadonnées (YAML)

```yaml
---
title: "Mon Cours RMarkdown"
author: "Nom de l'auteur"
output: word_document
---
```

2. Syntaxe de base pour les chunks de code R

```{r}
# Ceci est un chunk de code R
summary(iris)
```

3. Ajouter des titres
   
```
# Titre 1
## Sous-titre 2
```

4. Texte en gras ou en italique

```
*Texte en italique*
**Texte en gras**
```

5. Insérer des variables R dans des commentaires de texte

La taille moyenne des pétales est ``r mean(iris$Petal.Length)\``.

6. Options principales des chunks de code

- **`echo`** : Affiche ou non le code.
- **`eval`** : Exécute ou non le code.
- **`warning`** : Affiche ou non les warnings.
- **`message`** : Affiche ou non les messages.

```{r, eval=FALSE}
install.packages("knitr")
```

7. Créer des tableaux élégants avec `kable`

```{r, echo=FALSE}
library(knitr)
kable(head(iris), caption = "Tableau des premières lignes du jeu de données iris")
```

8. Utilisation de variables R dans les chunks

```{r}
mean_petal_length <- mean(iris$Petal.Length)
```

La longueur moyenne des pétales est : ``r mean_petal_length``.

9. Paramètres en en-tête de métadonnées (YAML)

```yaml
---
title: "Mon Cours RMarkdown"
author: "Nom de l'auteur"
date: "`r Sys.Date()`"
output: word_document
params:
  mon_parametre: "Sepal.Width"
---
```

:bulb: La fonction `get(param)` permet d'accéder dynamiquement à la colonne du jeu de données iris correspondant au paramètre passé.

```{r}
# Chargement du jeu de données iris et de ggplot2
library(ggplot2)

# Récupérer le paramètre passé dans le YAML
param <- params$mon_parametre

# Créer un boxplot en croisant la variable Species et le paramètre
ggplot(iris, aes(x = Species, y = get(param))) + 
  geom_boxplot() +
  labs(y = param, title = paste("Boxplot de", param, "par Species"))
```

## Liens utiles

Voici quelques liens utiles :

- [Initiation au R Markdown](https://rmarkdown.rstudio.com/lesson-1.html)
- [Markdown Cheat Sheet](https://www.markdownguide.org/cheat-sheet/)