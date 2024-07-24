# Restaurants

## Exercice 1 

Nous devons ici modéliser un restaurant.
Un restaurant dispose d'un nom et d'une adresse, un seul et même restaurant peut se situer à cette adresse. Dans ce restaurant travaillent des employés qui peuvents être des commis, des serveurs, etc..
Les employés ont la possibilité de travailler dans plusieurs restaurants si ils le souhaitent.
Un restaurant peut avoir plusieurs lieux pour son service comme une terrasse ou encore une salle, chacun de ces lieux aura une capacité précise avant de recevoir un nombre maximum de client.
Ce restaurant aura une seule carte de plats/repas active à la fois mais celle ci pourra différer en fonction de la saison (Printemps, été, automne, hiver), chaque carte sera composées d'entrées, de plats et de désserts. 
Certains éléments d'une carte peuvent être les mêmes à travers les saisons.

Donnez les relations ainsi que les contraintes de clé primaire et de clé étrangère nécessaire pour implémenter cette base de données.

## Exercice 2 (Vous pouvez à partir de cet exercice utiliser la base de donnée postgreSQL pour effectuer les tests nécessaires)

Implémenter le schéma relationnel de l'exercice 1 grâce au language DDL. 

## Exercice 3

Ecrire les requêtes SQL permettant d’obtenir les résultats suivants :
- Tuples de la table ’restaurant’
- Liste des lieux pouvant accueillir plus de 50 personnes
- Liste des lieux pouvant accueillir de 50 à 100 personnes
- Liste des restaurants disposant d'une terrasse
- Liste des chef ayant pour première lettre de leur nom le 'z'
- Liste de l'ensemble des serveurs travaillant au resturant "Les P'tites côtes"
