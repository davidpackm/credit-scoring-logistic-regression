# Credit Scoring par régression logistique | Prédiction de l’acceptation ou du refus d’une demande de crédit

## Présentation

Ce projet consiste à développer un modèle de **régression logistique** permettant de prédire l’**acceptation** ou le **refus** d’une demande de crédit à la consommation.

À partir des caractéristiques socio-économiques et financières des demandeurs, l’objectif est d’automatiser une décision de crédit à l’aide d’une méthode statistique interprétable et adaptée à une cible binaire.

## Contexte métier

**Astra Personal Finance** est une société de crédit à la consommation qui propose des financements à des fins personnelles, familiales ou domestiques. Les prêts accordés sont en espèces et **ne sont pas garantis**.

Dans ce contexte, la qualité de l’évaluation des dossiers est déterminante. Une mauvaise décision peut soit exposer l’entreprise à un risque excessif, soit conduire au refus de dossiers potentiellement acceptables.

Le service des demandes de crédit souhaite donc disposer d’un modèle capable de **prédire la décision d’acceptation ou de refus** d’une demande à partir des informations disponibles au moment de l’instruction du dossier.

## Objectif du projet

L’objectif du projet est de construire un modèle de classification capable de :

- prédire l’acceptation ou le refus d’une demande de crédit ;
- identifier les variables les plus liées à cette décision ;
- proposer un outil d’aide à la décision simple à interpréter.

## Données

Le projet repose sur **4446 cas réels** provenant d’**Astra Personal Finance**.

Les données décrivent le profil du demandeur ainsi que sa situation financière, avec notamment les variables suivantes :

- `Income` : revenu ;
- `Seniority` : ancienneté dans le poste ;
- `Marital` : état matrimonial ;
- `Home` : situation de logement ;
- `Job` : type d’emploi ;
- `Expenses` : charges ;
- `Assets` : actifs ;
- `Debt` : dette ;
- `Amount` : montant du prêt demandé ;
- `Price` : prix du bien ou de l’opération ;
- `Age` : âge.

La variable cible est :

- `Decision` : **acceptation** ou **refus** de la demande de crédit.

## Méthodologie

Le projet suit les étapes suivantes :

1. chargement et exploration des données ;
2. re-définition des catégories de référence pour certaines variables qualitatives ;
3. découpage du jeu de données en un échantillon d’entraînement et un échantillon de test ;
4. estimation d’un modèle de régression logistique binaire ;
5. prédiction des probabilités sur l’échantillon test ;
6. transformation des probabilités en décisions binaires à l’aide d’un seuil de 0,5 ;
7. évaluation du modèle à partir de l’accuracy et de la matrice de confusion.

## Modèle utilisé

Le modèle estimé est une **régression logistique binaire** avec lien logit :

La régression logistique a été retenue car elle est :

- adaptée à une cible binaire ;
- interprétable ;
- largement utilisée dans les problématiques de scoring et de décision de crédit.

## Variables du modèle

Le modèle final inclut les variables suivantes :

- `Seniority`
- `Home`
- `Marital`
- `Age`
- `Job`
- `Expenses`
- `Income`
- `Assets`
- `Debt`
- `Amount`
- `Price`

## Découpage apprentissage / test

Le jeu de données a été séparé en deux sous-ensembles :

- **jeu d’entraînement** : 2980 observations ;
- **jeu de test** : 1466 observations.

Le modèle est estimé sur le jeu d’entraînement, puis évalué sur le jeu de test.

## Résultats

### Performance globale

Le modèle atteint une **accuracy de 0,77** sur l’échantillon test.

Autrement dit, **77 % des décisions sont correctement prédites** sur les données de test.

### Matrice de confusion

|                       | Rejeté (réel) | Accepté (réel) |
|-----------------------|--------------:|---------------:|
| **Prédit rejet**      | 172           | 86             |
| **Prédit acceptation**| 252           | 956            |

### Lecture rapide des résultats

- **956 dossiers acceptés** sont correctement prédits comme acceptés ;
- **172 dossiers rejetés** sont correctement prédits comme rejetés ;
- **252 dossiers rejetés** sont prédits à tort comme acceptés ;
- **86 dossiers acceptés** sont prédits à tort comme rejetés.

Le modèle est donc **plus performant pour reconnaître les dossiers acceptés** que pour détecter les dossiers rejetés.

## Interprétation de quelques résultats du modèle

L’estimation met en évidence plusieurs effets cohérents avec une logique de décision de crédit :

- une **ancienneté plus élevée** (`Seniority`) est associée à une probabilité plus forte d’acceptation ;
- un **revenu plus élevé** (`Income`) augmente la probabilité d’acceptation ;
- des **charges plus élevées** (`Expenses`) réduisent la probabilité d’acceptation ;
- une **dette plus élevée** (`Debt`) réduit la probabilité d’acceptation ;
- un **montant demandé plus important** (`Amount`) est associé à une probabilité plus faible d’acceptation ;
- certains statuts professionnels comme **part-time** ou **freelance** sont associés à une probabilité plus faible d’acceptation relativement à la catégorie de référence ;
- le fait d’être **propriétaire** (`Homeowner`) est associé à une probabilité plus élevée d’acceptation par rapport à la référence.

Ces résultats renforcent l’intérêt de la régression logistique comme outil de scoring interprétable.

## Exemple d’utilisation

Le projet inclut également une prédiction sur un dossier individuel à partir d’un profil défini manuellement :

- ancienneté : 5 ans ;
- logement : propriétaire ;
- état matrimonial : célibataire ;
- âge : 50 ans ;
- emploi : freelance ;
- charges : 50 ;
- revenu : 300 ;
- actifs : 0 ;
- dette : 0 ;
- montant demandé : 500 ;
- prix : 400.

Le modèle renvoie alors une **probabilité d’acceptation**, pouvant être utilisée dans une logique d’aide à la décision.

## Outils utilisés

- **R**
- `glm()` pour l’estimation de la régression logistique
- fonctions de base R pour :
  - la préparation des données ;
  - la prédiction ;
  - l’évaluation ;
  - la visualisation de la matrice de confusion

## Compétences mobilisées

- préparation de données ;
- gestion de variables qualitatives ;
- modélisation statistique binaire ;
- interprétation d’une régression logistique ;
- évaluation d’un classifieur ;
- application de méthodes quantitatives à une problématique de crédit.

## Limites

Ce projet repose sur une approche simple et interprétable, mais plusieurs prolongements sont possibles :

- étudier plus finement le choix du seuil de décision ;
- calculer des métriques complémentaires comme la précision, le rappel ou l’AUC ;
- comparer la régression logistique à d’autres méthodes de classification ;
- mieux traiter l’asymétrie de coût entre les erreurs de type acceptation à tort et refus à tort.
