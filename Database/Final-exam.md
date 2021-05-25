# Club de sport

## Exercice 1 

Il existe plusieurs centaines de club de sport en france, chacun caractérisé par sa localisation, son sport et le nombre d'adhérent du club.
Un adhérent ne peut appartenir qu'à un seul club à la fois, chaque adhérent est reconnu par son nom, prénom et son numéro de license.
Un sport est caractérisé par son nom, son lieu de pratique ainsi que le nombre de joueur nécessaire pour y jouer. Un lieu de pratique 
peut prendre plusieurs valeurs (Intérieurs, extérieurs, gazon, terre battue, ...), un sport peut également être joué sur plusieurs type de lieu de pratique.

Donnez les relations ainsi que les contraintes de clé primaire et de clé étrangère nécessaire pour implémenter cette base de données.

## Exercice 2 (Vous pouvez à partir de cet exercice utiliser la base de donnée postgreSQL pour effectuer les tests nécessaires)

Implémenter le schéma relationnel de l'exercice 1 grâce au language DDL. 

## Exercice 3

Ecrire les requêtes SQL permettant d’obtenir les résultats suivants :
- Tuples de la table ’club’
- Liste des sports ayant besoin de plus de 5 joueurs
- Liste des sports ayant besoin de 5 à 10 joueurs
- Liste des sports pouvant être joués sur plusieurs lieux de pratiques
- Liste des joueurs ayant pour première lettre de leur nom le 'z'
- Liste de l'ensemble des joueurs du club de Gravelines
