# Chapitre 5 : Initiation au R Shiny

- [Chapitre 5 : Initiation au R Shiny](#chapitre-5--initiation-au-r-shiny)
  - [Objectifs](#objectifs)
  - [Création d'un projet Shiny dans RStudio](#création-dun-projet-shiny-dans-rstudio)
    - [Étapes pour créer un projet Shiny](#étapes-pour-créer-un-projet-shiny)
    - [Structure d’une application Shiny (`app.R` ou `ui.R` + `server.R`)](#structure-dune-application-shiny-appr-ou-uir--serverr)
      - [Fichier unique : `app.R`](#fichier-unique--appr)
      - [Fichiers séparés : `ui.R` et `server.R`](#fichiers-séparés--uir-et-serverr)
  - [Les objets réactifs dans Shiny](#les-objets-réactifs-dans-shiny)
    - [Ajouter un objet réactif dans l’UI](#ajouter-un-objet-réactif-dans-lui)
    - [Définir la logique réactive dans le serveur](#définir-la-logique-réactive-dans-le-serveur)
  - [Gérer les différents layouts Shiny](#gérer-les-différents-layouts-shiny)
    - [`fluidPage()`](#fluidpage)
    - [`sidebarLayout()`](#sidebarlayout)
    - [`splitLayout()`](#splitlayout)
    - [`navbarPage()` et `tabPanel()`](#navbarpage-et-tabpanel)
    - [`fluidRow()` et `column()`](#fluidrow-et-column)
  - [Les widgets Shiny](#les-widgets-shiny)
    - [Boutons](#boutons)
    - [Checkbox unique](#checkbox-unique)
    - [Checkbox group](#checkbox-group)
    - [Date input](#date-input)
    - [Date range input](#date-range-input)
    - [File input](#file-input)
    - [Numeric input](#numeric-input)
    - [Radio buttons](#radio-buttons)
    - [Select box](#select-box)
    - [Sliders](#sliders)
    - [Text input](#text-input)
    - [Récapitulatif](#récapitulatif)
  - [Afficher des tableaux dans Shiny](#afficher-des-tableaux-dans-shiny)
    - [Tableau simple avec `tableOutput`](#tableau-simple-avec-tableoutput)
    - [Tableau avec `DT::renderDT` pour interactivité](#tableau-avec-dtrenderdt-pour-interactivité)
    - [Tableau récapitulatif des options](#tableau-récapitulatif-des-options)
  - [Pourquoi utiliser la syntaxe votre\_package::fonction](#pourquoi-utiliser-la-syntaxe-votre_packagefonction)
  - [Ajouter des images dans Shiny](#ajouter-des-images-dans-shiny)
    - [Images dans le projet Shiny](#images-dans-le-projet-shiny)
    - [Images depuis une URL web](#images-depuis-une-url-web)
  - [Créer des graphiques interactifs avec esquisse et plotly](#créer-des-graphiques-interactifs-avec-esquisse-et-plotly)
    - [Esquisse : créer le graphique hors Shiny](#esquisse--créer-le-graphique-hors-shiny)
    - [Plotly : rendre le graphique interactif dans Shiny](#plotly--rendre-le-graphique-interactif-dans-shiny)
  - [Déployer une application sur shinyapps.io](#déployer-une-application-sur-shinyappsio)
    - [Prérequis](#prérequis)
    - [Se connecter depuis R](#se-connecter-depuis-r)
    - [Déployer l’application](#déployer-lapplication)
    - [Limitations de la version gratuite](#limitations-de-la-version-gratuite)
    - [Bonnes pratiques](#bonnes-pratiques)
  - [Aller plus loin](#aller-plus-loin)
  - [Liens utiles](#liens-utiles)


## Objectifs

Voici les objectifs de ce module :
- [x] Créer un projet Shiny et comprendre sa structure (app.R / ui.R + server.R)  
- [x] Utiliser et organiser les layouts Shiny
- [x] Ajouter et configurer des widgets interactifs
- [x] Afficher des graphiques et tableaux interactifs
- [x] Intégrer des images locales et web en utilisant des chemins relatifs  
- [x] Utiliser package::fonction pour un code clair et reproductible


## Création d'un projet Shiny dans RStudio

Shiny est un package R permettant de créer des **applications web interactives** directement à partir de R.  

### Étapes pour créer un projet Shiny

1. Ouvrir **RStudio**.
2. Aller dans **File → New Project → New Directory → Shiny Web Application**.
3. Donner un **nom** au projet et choisir l’**emplacement** sur votre disque.
4. Choisir si vous voulez un **fichier unique (`app.R`)** ou deux fichiers séparés (`ui.R` et `server.R`).  
5. Cliquer sur **Create Project**.  
6. RStudio génère automatiquement les fichiers nécessaires avec un exemple minimal de Shiny.  

:bulb: Dans un projet R Shiny, toujours travailler dans un **projet RStudio** pour organiser correctement les fichiers, les données et les dépendances.

### Structure d’une application Shiny (`app.R` ou `ui.R` + `server.R`)

Une application Shiny peut être structurée de deux façons :

#### Fichier unique : `app.R`

- Contient **toutes les parties de l’application** dans un seul fichier :
  - `ui` → l’interface utilisateur (ce que voit l’utilisateur)
  - `server` → la logique serveur (les calculs et réactions)
  - `shinyApp(ui, server)` → relie les deux et lance l’application

#### Fichiers séparés : `ui.R` et `server.R`

- `ui.R` → définit l’interface utilisateur
- `server.R` → contient le code serveur
- Avantage : **plus facile à organiser** pour les applications complexes
- RStudio combine automatiquement les deux fichiers pour exécuter l’application.

:bulb: Dans les deux cas, la structure reste la même : **interface + logique serveur**.

## Les objets réactifs dans Shiny

Dans Shiny, un **objet réactif** est un élément de sortie qui se met à jour automatiquement lorsque ses **données ou widgets associés changent**.  
La création d’un objet réactif se fait en **deux étapes** : ajouter l’objet dans l’UI, puis définir sa logique dans le serveur.

### Ajouter un objet réactif dans l’UI

Shiny propose des fonctions `*Output` pour afficher différents types d’objets :

| Output function | Crée |
|-----------------|------|
| dataTableOutput  | DataTable |
| htmlOutput       | HTML brut |
| imageOutput      | image |
| plotOutput       | graphique |
| tableOutput      | tableau |
| textOutput       | texte |
| uiOutput         | HTML ou tag Shiny |
| verbatimTextOutput | texte formaté |

```r
ui <- fluidPage(
  titlePanel("Histogramme réactif"),
  sidebarLayout(
    sidebarPanel(
      sliderInput("bins", "Nombre de bins :", min = 1, max = 50, value = 30)
    ),
    mainPanel(
      plotOutput("distPlot")
    )
  )
)
```

:bulb:
- Chaque fonction `*Output` prend un **argument : un nom de caractère** qui identifie l’objet réactif.  
- Les utilisateurs ne voient pas ce nom, il est utilisé pour référencer l’objet dans le serveur.

### Définir la logique réactive dans le serveur

Chaque objet réactif est construit dans la fonction `server` via `output$nom_objet <- render*({ ... })`.  
Le nom doit correspondre au nom donné dans l’UI.

```r
server <- function(input, output) {
  output$distPlot <- renderPlot({
    x <- faithful$waiting   # Utilisation du dataset intégrée faithful
    bins <- seq(min(x), max(x), length.out = input$bins + 1)
    hist(x, breaks = bins, col = "darkgray", border = "white",
         main = "Histogramme de temps d’attente des geysers",
         xlab = "Temps d’attente (minutes)")
  })
}
shinyApp(ui = ui, server = server)
```

:bulb:
- Les fonctions `render*` correspondent au type d’objet :  

| Render function | Crée |
|-----------------|------|
| renderDataTable  | DataTable |
| renderImage      | image (depuis un fichier ou URL) |
| renderPlot       | graphique |
| renderPrint      | tout objet imprimé |
| renderTable      | data frame, matrice ou tableau |
| renderText       | chaîne de caractères |
| renderUI         | tag Shiny ou HTML |

- L’expression passée à `render*` est évaluée **lors du lancement de l’application** et **à chaque mise à jour** des widgets associés.  
- L’expression doit **retourner un objet du bon type** sinon Shiny générera une erreur.
- Pensez à **toujours faire correspondre le nom de `output$...` dans le serveur** avec celui de `*Output` dans l’UI.  
- Les objets réactifs permettent de créer des **applications dynamiques** où le contenu s’adapte automatiquement aux interactions de l’utilisateur.

## Gérer les différents layouts Shiny

Shiny propose plusieurs **manières d’organiser l’interface** afin de structurer les éléments de l’application.


### `fluidPage()`

- Crée une page **responsive**, adaptée à toutes les tailles d’écran
- Les éléments sont organisés **verticalement**
- Exemple d’usage typique : ajouter des titres, des inputs, des outputs

```r
ui <- fluidPage(
  titlePanel("Exemple fluidPage"),
  p("Texte explicatif"),
  plotOutput("plot1")
)

server <- function(input, output) {
  output$plot1 <- renderPlot({
    plot(rnorm(50), rnorm(50))
  })
}
```

### `sidebarLayout()`

- Combine une **barre latérale** et une **zone principale**
- La **sidebar** contient souvent des filtres ou contrôles (`input`)
- La **main panel** affiche les résultats ou graphiques (`output`)

```r
ui <- fluidPage(
  sidebarLayout(
    sidebarPanel(
      selectInput("variable", "Choisir une variable :", choices = names(iris))
    ),
    mainPanel(
      plotOutput("graph")
    )
  )
)

server <- function(input, output) {
  output$graph <- renderPlot({
    var <- input$variable
    plot(iris[[var]], main = paste("Histogramme de", var))
  })
}
```

### `splitLayout()`

- Permet de créer une **mise en page horizontale**, avec plusieurs colonnes côte à côte
- Utile pour comparer graphiques ou tableaux simultanément

```r
ui <- fluidPage(
  splitLayout(
    plotOutput("graph1"),
    plotOutput("graph2")
  )
)

server <- function(input, output) {
  output$graph1 <- renderPlot({ plot(rnorm(50)) })
  output$graph2 <- renderPlot({ plot(runif(50)) })
}
```

### `navbarPage()` et `tabPanel()`

- `navbarPage()` → crée une **navigation par onglets** en haut de la page
- Chaque onglet est défini avec `tabPanel()`
- Idéal pour **séparer les sections** ou fonctionnalités d’une application

```r
ui <- navbarPage("Mon application",
  tabPanel("Résumé", p("Résumé des données"), tableOutput("table1")),
  tabPanel("Graphique", plotOutput("graph")),
  tabPanel("Tableau", tableOutput("table2"))
)

server <- function(input, output) {
  output$graph <- renderPlot({ plot(rnorm(50), rnorm(50)) })
  output$table1 <- renderTable({ head(iris) })
  output$table2 <- renderTable({ summary(iris) })
}
```

### `fluidRow()` et `column()`

- Permet de **diviser l’espace horizontalement** dans une page `fluidPage()`
- Chaque `column(width = x)` occupe une fraction de la largeur totale (12 = pleine largeur)
- Combine plusieurs colonnes pour créer des mises en page **flexibles** et **alignées**

```r
ui <- fluidPage(
  fluidRow(
    column(4, sliderInput("n", "Nombre de points :", 1, 100, 50)),
    column(4, plotOutput("graph")),
    column(4, tableOutput("table"))
  )
)

server <- function(input, output) {
  output$graph <- renderPlot({ plot(runif(input$n), runif(input$n)) })
  output$table <- renderTable({ head(iris, n = input$n) })
}
```


:warning:

- `fluidPage()` est le conteneur principal
- Les autres layouts (`sidebarLayout`, `splitLayout`, `navbarPage`, `fluidRow`) s’imbriquent à l’intérieur pour organiser l’interface selon le besoin

## Les widgets Shiny

Shiny propose de nombreux **widgets interactifs** pour construire des interfaces utilisateur.  

:bulb:
- Tous les widgets utilisent des **identifiants uniques** (`inputId`) pour être récupérés côté serveur avec `input$inputId`.  
- Ces widgets peuvent être combinés dans des **layouts Shiny** (`fluidPage`, `sidebarLayout`, `splitLayout`, `navbarPage`, `fluidRow`) pour créer des interfaces complètes.

### Boutons

```r
ui <- fluidPage(
  titlePanel("Boutons Shiny"),
  actionButton("action", "Action"),
  submitButton("Submit"),
  verbatimTextOutput("out")
)

server <- function(input, output) {
  output$out <- renderPrint({
    input$action
  })
}

shinyApp(ui = ui, server = server)
```

### Checkbox unique

```r
ui <- fluidPage(
  titlePanel("Checkbox unique"),
  checkboxInput("checkbox", "Choice A", value = TRUE),
  verbatimTextOutput("out")
)

server <- function(input, output) {
  output$out <- renderPrint({
    input$checkbox
  })
}

shinyApp(ui = ui, server = server)
```

### Checkbox group

```r
ui <- fluidPage(
  titlePanel("Checkbox group"),
  checkboxGroupInput("checkGroup", "Select all that apply",
                     choices = list("Choice 1" = 1, "Choice 2" = 2, "Choice 3" = 3),
                     selected = 1),
  verbatimTextOutput("out")
)

server <- function(input, output) {
  output$out <- renderPrint({
    input$checkGroup
  })
}

shinyApp(ui = ui, server = server)
```

### Date input

```r
ui <- fluidPage(
  titlePanel("Date input"),
  dateInput("date", "Select date", value = "2014-01-01"),
  verbatimTextOutput("out")
)

server <- function(input, output) {
  output$out <- renderPrint({
    input$date
  })
}

shinyApp(ui = ui, server = server)
```

### Date range input

```r
ui <- fluidPage(
  titlePanel("Date range input"),
  dateRangeInput("dates", "Select dates"),
  verbatimTextOutput("out")
)

server <- function(input, output) {
  output$out <- renderPrint({
    input$dates
  })
}

shinyApp(ui = ui, server = server)
```

### File input

```r
ui <- fluidPage(
  titlePanel("File input"),
  fileInput("file", label = NULL),
  verbatimTextOutput("out")
)

server <- function(input, output) {
  output$out <- renderPrint({
    input$file
  })
}

shinyApp(ui = ui, server = server)
```

### Numeric input

```r
ui <- fluidPage(
  titlePanel("Numeric input"),
  numericInput("num", "Input number", value = 1),
  verbatimTextOutput("out")
)

server <- function(input, output) {
  output$out <- renderPrint({
    input$num
  })
}

shinyApp(ui = ui, server = server)
```

### Radio buttons

```r
ui <- fluidPage(
  titlePanel("Radio buttons"),
  radioButtons("radio", "Select option",
               choices = list("Choice 1" = 1, "Choice 2" = 2, "Choice 3" = 3),
               selected = 1),
  verbatimTextOutput("out")
)

server <- function(input, output) {
  output$out <- renderPrint({
    input$radio
  })
}

shinyApp(ui = ui, server = server)
```

### Select box

```r
ui <- fluidPage(
  titlePanel("Select box"),
  selectInput("select", "Select option",
              choices = list("Choice 1" = 1, "Choice 2" = 2, "Choice 3" = 3),
              selected = 1),
  verbatimTextOutput("out")
)

server <- function(input, output) {
  output$out <- renderPrint({
    input$select
  })
}

shinyApp(ui = ui, server = server)
```

### Sliders

```r
ui <- fluidPage(
  titlePanel("Sliders"),
  sliderInput("slider1", "Set value", min = 0, max = 100, value = 50),
  sliderInput("slider2", "Set value range", min = 0, max = 100, value = c(25, 75)),
  verbatimTextOutput("out1"),
  verbatimTextOutput("out2")
)

server <- function(input, output) {
  output$out1 <- renderPrint({ input$slider1 })
  output$out2 <- renderPrint({ input$slider2 })
}

shinyApp(ui = ui, server = server)
```

### Text input

```r
ui <- fluidPage(
  titlePanel("Text input"),
  textInput("text", label = NULL, value = "Enter text..."),
  verbatimTextOutput("out")
)

server <- function(input, output) {
  output$out <- renderPrint({
    input$text
  })
}

shinyApp(ui = ui, server = server)
```


### Récapitulatif

Voici un tableau récapitulatif avec un **exemple de code simple** pour chacun.

| Widget | Description | Exemple de code |
|--------|-------------|----------------|
| **Boutons** | Permettent de déclencher des actions côté serveur | actionButton("action", "Action") <br> submitButton("Submit") |
| **Checkbox unique** | Case à cocher simple (TRUE/FALSE) | checkboxInput("checkbox", "Choice A", value = TRUE) |
| **Checkbox group** | Groupe de cases à cocher, possibilité de sélectionner plusieurs options | checkboxGroupInput("checkGroup", "Select all that apply", choices = list("Choice 1" = 1, "Choice 2" = 2, "Choice 3" = 3), selected = 1) |
| **Date input** | Permet de sélectionner une date unique | dateInput("date", "Select date", value = "2014-01-01") |
| **Date range input** | Permet de sélectionner une plage de dates | dateRangeInput("dates", "Select dates") |
| **File input** | Permet de téléverser un fichier | fileInput("file", label = NULL) |
| **Help text** | Texte d’aide, non interactif | helpText("Note: help text isn't a true widget, but it provides an easy way to add text to accompany other widgets.") |
| **Numeric input** | Entrée numérique avec valeur par défaut | numericInput("num", "Input number", value = 1) |
| **Radio buttons** | Permet de sélectionner une option parmi plusieurs | radioButtons("radio", "Select option", choices = list("Choice 1" = 1, "Choice 2" = 2, "Choice 3" = 3), selected = 1) |
| **Select box** | Menu déroulant pour choisir une option | selectInput("select", "Select option", choices = list("Choice 1" = 1, "Choice 2" = 2, "Choice 3" = 3), selected = 1) |
| **Slider simple** | Curseur pour choisir une valeur unique | sliderInput("slider1", "Set value", min = 0, max = 100, value = 50) |
| **Slider range** | Curseur pour choisir une plage de valeurs | sliderInput("slider2", "Set value range", min = 0, max = 100, value = c(25, 75)) |
| **Text input** | Champ texte libre | textInput("text", label = NULL, value = "Enter text...") |


## Afficher des tableaux dans Shiny

Shiny permet d’afficher des tableaux de données interactifs ou statiques à l’aide de `tableOutput` et `renderTable`.  
On peut aussi utiliser des packages comme `DT` pour des tableaux plus avancés.


### Tableau simple avec `tableOutput`

- `tableOutput` est utilisé dans l’UI pour réserver l’espace du tableau.  
- `renderTable` est utilisé dans le serveur pour afficher les données.

```r
ui <- fluidPage(
  titlePanel("Tableau simple"),
  tableOutput("table1")
)

server <- function(input, output) {
  output$table1 <- renderTable({
    head(iris)
  })
}

shinyApp(ui = ui, server = server)
```

### Tableau avec `DT::renderDT` pour interactivité

- `DT` permet d’avoir des tableaux **triables, filtrables et paginés**.

```r
ui <- fluidPage(
  titlePanel("Tableau interactif"),
  DT::DTOutput("tableDT")
)

server <- function(input, output) {
  output$tableDT <- DT::renderDT({
    DT::datatable(iris)
  })
}

shinyApp(ui = ui, server = server)
```

:bulb:

- Pour utiliser `DT`, il faut installer le package `DT` (`install.packages("DT")`).  
- Les tableaux interactifs sont très pratiques pour de grandes bases de données.

### Tableau récapitulatif des options

| Fonction | Description | Exemple |
|----------|------------|---------|
| tableOutput() | Réserve l’espace pour un tableau | tableOutput("table1") |
| renderTable() | Génère un tableau simple côté serveur | renderTable(head(iris)) |
| DTOutput() | Réserve l’espace pour un tableau interactif | DT::DTOutput("tableDT") |
| renderDT() | Génère un tableau interactif côté serveur | DT::renderDT(DT::datatable(iris)) |

:bulb:
- Pour un **rapport rapide**, tableOutput + renderTable suffit.  
- Pour de **grandes tables** ou des tableaux interactifs, préférez `DT`.

## Pourquoi utiliser la syntaxe votre_package::fonction

En R, on peut appeler une fonction directement depuis un package sans l’avoir chargé avec `library()` en utilisant la syntaxe `votre_package::fonction`.  

- Permet d’éviter **les conflits de noms** si plusieurs packages ont une fonction du même nom.
- Utile pour écrire des **scripts reproductibles**, car on sait exactement de quel package provient la fonction.
- Permet d’utiliser une fonction ponctuellement **sans charger tout le package**.
- Pour des packages lourds ou peu utilisés, `votre_package::fonction` permet de **gagner du temps et d’éviter des chargements inutiles

## Ajouter des images dans Shiny

Dans Shiny, il est courant d’ajouter des images pour illustrer vos applications.  

### Images dans le projet Shiny

- Placer vos images dans un **dossier `www`** à la racine du projet Shiny.
- Utiliser la fonction `img()` pour afficher l’image dans l’UI.

```r
ui <- fluidPage(
  titlePanel("Image locale"),
  img(src = "www/mon_image.png", height = "200px")
)
```

:bulb:  

- Shiny sert automatiquement le contenu du dossier `www`.  
- Toujours utiliser un **chemin relatif** (`./www/mon_image.png`) plutôt qu’un chemin absolu (`C:/Documents/TOTO/.../.../www/mon_image.png`) pour que l’application fonctionne sur d’autres ordinateurs.


### Images depuis une URL web

Vous pouvez afficher directement une image accessible en ligne en utilisant son URL.

```r
ui <- fluidPage(
  titlePanel("Image web"),
  img(src = "https://upload.wikimedia.org/wikipedia/fr/thumb/4/4e/RStudio_Logo.png/1024px-RStudio_Logo.png", height = "200px")
)
```

:bulb:
- Vérifiez que l’URL est valide et accessible depuis tous les utilisateurs.  
- Cette méthode ne nécessite pas de copier l’image dans le projet.


## Créer des graphiques interactifs avec esquisse et plotly

Pour intégrer des graphiques interactifs dans Shiny, il est pratique de **séparer la création du graphique et l’interactivité** :

1. **Esquisse** pour créer rapidement un graphique et récupérer le code `ggplot2`.  
2. **Plotly** pour transformer ce graphique en graphique interactif dans Shiny.

### Esquisse : créer le graphique hors Shiny

- Installer le package si nécessaire :

```r
install.packages("esquisse")
```

```r
library(esquisse)
library(ggplot2)
# Lancer l’interface esquisse
esquisser(iris)
```

:bulb:  
- Esquisse ouvre une **interface graphique** où vous pouvez **glisser-déposer les variables**, choisir le type de graphique et visualiser le résultat.  
- Une fois satisfait, **copier le code `ggplot2` généré** pour l’intégrer dans votre application Shiny.

```r
p <- ggplot(iris, aes(x = Sepal.Length, y = Sepal.Width, color = Species)) +
  geom_point() +
  theme_minimal()
```

### Plotly : rendre le graphique interactif dans Shiny

```r
install.packages("plotly")
```

```r
library(shiny)
library(plotly)
library(ggplot2)

ui <- fluidPage(
  titlePanel("Graphique interactif avec plotly"),
  plotlyOutput("plot1")
)

server <- function(input, output) {
  output$plot1 <- renderPlotly({
    # Code ggplot2 récupéré depuis esquisse
    p <- ggplot(iris, aes(x = Sepal.Length, y = Sepal.Width, color = Species)) +
      geom_point() +
      theme_minimal()
    ggplotly(p)   # transforme le ggplot en graphique interactif
  })
}

shinyApp(ui = ui, server = server)
```

:bulb:

- Esquisse sert **uniquement à prototyper et générer le code ggplot2**, vous n’avez pas besoin de l’utiliser dans Shiny.  
- `ggplotly()` ajoute automatiquement **zoom, hover et légende interactive**.  
- Vous pouvez combiner ce graphique avec **des widgets Shiny** pour le rendre dynamique (filtrage, sélection, etc.).

## Déployer une application sur shinyapps.io

ShinyApps.io est le service officiel de RStudio pour **héberger et partager vos applications Shiny en ligne**.  
Il permet de rendre vos applications accessibles via un simple navigateur, sans que l’utilisateur ait besoin d’installer R ou Shiny.

### Prérequis

- Installer le package `rsconnect` :
  
```r
install.packages("rsconnect")
```

- Créer un compte sur [https://www.shinyapps.io](https://www.shinyapps.io)
- Récupérer vos **identifiants (token et secret)** dans le tableau de bord ShinyApps.io

### Se connecter depuis R

library(rsconnect)

rsconnect::setAccountInfo(name='votre_nom',
                          token='votre_token',
                          secret='votre_secret')

:bulb: Une seule fois suffit, ensuite R se souviendra de vos informations pour vos déploiements futurs.

### Déployer l’application

- Placer **tous les fichiers nécessaires** dans le même dossier :  
  - `app.R` ou `ui.R + server.R`  
  - Dossier `www` pour les images, CSS, etc.  
  - Fichiers de données utilisés  

- Déployer avec :

```r
rsconnect::deployApp("chemin/vers/votre/app")
```

- Une URL publique sera générée, par exemple :  
  `https://votre_nom.shinyapps.io/monapp`

### Limitations de la version gratuite

- **Nombre d’applications actives limité** : 5 applications maximum
- **Nombre de connexions simultanées limité** : ~25 connexions simultanées par application
- **Temps d’inactivité** : les applications passent en veille après 15 minutes sans activité
- **Stockage limité** : taille totale du compte limitée
- **Ressources limitées** : CPU et mémoire réduites comparé à un serveur payant

### Bonnes pratiques

- Toujours tester localement l’application avant le déploiement
- Utiliser **des chemins relatifs** pour les fichiers et images
- Eviter les données trop volumineuses : mieux vaut charger les données depuis un fichier en ligne ou une base de données
- Documenter votre code et les packages nécessaires pour faciliter la maintenance


## Aller plus loin

Pour aller plus loin, vous pouvez consulter les liens utiles ci-dessous : 

## Liens utiles

Voici quelques liens utiles :

- [Initiation au R Shiny](https://shiny.posit.co/r/getstarted/shiny-basics/lesson1/index.html)