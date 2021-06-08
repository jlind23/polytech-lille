
## Avant de commencer
Quels sont les concepts de base du modèle relationel?

## En résumé
- **Attribut** : Colonne nommée d'une table. Le nom est unique au sein de la relation.
- **Domaine** : Ensemble de valeurs caractérisées par un nom.
- **Schéma de relation** : Ensemble d'attributs avec, pour chaque attribut, un domaine qui lui est associé.
- **Tuple** : Ensemble d'attributs associés aux valeurs appartenant à son domaine.
- **Relation** : Un schéma de relation et un ensemble de tuples associés à un nom.
- **Contrainte d'intégrité** : Assertion vérifiée par les données de la base à tout moment.
- **Clé primaire** : Contrainte sur une relation imposant l'unicité des valeurs d'un groupe d'attributs.
- **Clé étrangère** : Contrainte portant sur une relation R1 qui consiste à specifier que les valeurs d'un groupe d'attributs sont *un sous ensemble* des valeurs du groupe d'attributs relatif à la clé primaire d'une relation R2.

# SQL

## SQL
Structured Query Language, le langage de requêtes structuré.
Permet d'intéragir avec une base de données selon trois grands axes :

- Définition du schéma (Data Definition Language ou DDL)
- Manipulation des données (Data Manipulation Language ou DML)
- Gestion des droits (non abordé dans ce cours)

## SQL
Les commandes commencent par un mot clé servant à nommer l'opération de base à exécuter. Chaque commande SQL doit remplir deux exigences :

1. Indiquer la table (DDL) ou les données (DML) sur lesquelles elle opère
2. Indiquer l'opération à exécuter sur ces données

## Domaines fournis par défaut dans SQL
- Les numériques : INTEGER, DOUBLE, MONEY, ...

> exemple : `23`, `-122`, `3.4`, `-6.7`, ...

- Les alphanumériques : CHAR, TEXT, ...

> exemples : `'v'`, `'la vie est un long fleuve ...'`

- Le type DATE (format configurable)

> exemple : `2002-02-28`

- Le type boolean : BOOL

> exemples : `FALSE`, `TRUE`

- Et bien d'autres...

# Data Definition Language

## Data Definition Language
Permet de modifier le schéma de la base de données :

- Créer des tables
- Spécifier les clés primaires
- Spécifier les clés étrangères
- Supprimer des tables

## Créer une table - CREATE TABLE
Pour créer une table il faut spécifier :

1. Le nom de la table
2. Le nom et le type de chaque attribut

```sql
CREATE TABLE boisson (
	denomination TEXT,
	prix MONEY
);
```

## Spécifier une clé primaire
Il est possible de spécifier une clé primaire à la création de la table :

```sql
CREATE TABLE boisson (
	denomination TEXT,
	prix MONEY,
	PRIMARY KEY(denomination)
);
```

Si la clé primaire est formée de plusieurs attributs, les spécifier en les séparant par une virgule :

```sql
CREATE TABLE boisson (
	denomination TEXT,
	marque TEXT,
	prix MONEY,
	PRIMARY KEY(denomination, marque)
);
```

## Spécifier une clé étrangère (1/2)
Il est possible de spécifier une clé étrangère à la création de la table :

```sql
CREATE TABLE personne (
	id INTEGER PRIMARY KEY,
	nom TEXT,
	prenom TEXT,
	preference TEXT,
	FOREIGN KEY (preference)
		REFERENCES boisson(denomination)
);
```

## Spécifier une clé étrangère (2/2)
Si la clé primaire référencée est formée de plusieurs attributs, les spécifier en les séparant par une virgule :

```sql
CREATE TABLE personne (
	id INTEGER PRIMARY KEY,
	nom TEXT,
	prenom TEXT,
	preference TEXT,
	marque_preference TEXT,
	FOREIGN KEY (preference, marque_preference)
		REFERENCES boisson(denomination, marque)
);
```

## Supprimer une table - DROP TABLE
Pour supprimer une table, il suffit d'utiliser la commande `DROP TABLE` suivie du nom de la table :

```sql
DROP TABLE personne;
```

# Activités

## Activité 1

Implémenter le schéma relationnel de l'exercice "Entreprise de fabrication et de distribution".

## Activité 2
Voir feuille "Gestion d’une galerie de peinture".

# Data Manipulation Language

## Insérer des données
- L'insertion de données dans une table se fait via la requête `INSERT`.
- Paramétrée par:
	1. La table cible
	2. Les données à placer dans chaque colonne

## Exemple: INSERT
- Insérer la boisson 'Limonade' à 1,5 euro.

```sql
INSERT INTO boisson(denomination, prixunitaire)
VALUES ('Limonade', 1.5);
```

## Question: INSERT
Quelle requête permet d'insérer Bruno Aube dans la table `personne` en sachant que sa boisson préférée est le vin?

## Modifier des données
- La modification de données dans une table se fait via la requête `UPDATE`.
- Paramétrée par:
	1. La table cible
	2. Les données à modifier dans chaque colonne
	3. La condition de mise à jour d'une ligne

## Exemple: UPDATE
- Modifier le prix de la boisson 'Limonade' de 1,5 euro à 1,7 euro.

```sql
UPDATE boisson
SET prixunitaire=1.5
WHERE denomination='Limonade';
```

- Réduire de 50% le prix de la boisson 'Limonade'.

```sql
UPDATE boisson
SET prixunitaire=0.5*prixunitaire
WHERE denomination='Limonade';
```

## Question: UPDATE
Quelle requête permet de modifier la préférence en boisson de Bruno Aube dans la table `personne` pour devenir la limonade ?

## Supprimer des données
- La suppression de données dans une table se fait via la requête `DELETE`.
- Paramétrée par:
	1. La table cible
	2. La condition de suppression d'une ligne

## Exemple: DELETE
- Supprimer la boisson 'Limonade'.

```sql
DELETE FROM boisson
WHERE denomination='Limonade';
```

## Question: DELETE
- Quelle requête permet de supprimer Bruno Aube de la table `personne` ?
- Quelle requête permet de supprimer toutes les personnes ayant comme boisson préférée le vin de la table `personne` ?

## Interroger une base de données
- L'interrogation de la base de données se fait via la requête `SELECT`.
- Requête plus complexe que celles d'insertion, modification et suppression de données.
- Possibilité d'imbriquer les requêtes `SELECT`.
- Retourne une table contenant les résultats.
- Paramétrée par:
	1. Les tables depuis lesquelles les données vont être lues
	2. La condition de sélection des lignes
	3. Les colonnes à sélectionner dans la table résultante
	4. ...

## Requête SELECT - Clause FROM
- Spécifie le nom des tables depuis lesquelles les données vont être lues.
- Si plusieurs tables sont spécifiées, le produit cartésien entre toutes ces tables est réalisé.
- Il s'agit de toutes les combinaisons entre les tuples des tables impliquées.

> *Cette clause doit obligatoirement être présente*.

Exemple : Lire les données depuis les tables `personne` et `boisson`.

```sql
[...]
FROM personne, boisson
[...]
```

## Produit cartésien: illustration
Produit cartésien des tuples de la table personne et de la table boisson:

![Produit cartésien](cartesian-product.pdf)

## Requête SELECT - Clause WHERE
- Spécifie la condition de sélection des lignes issues de la clause `FROM`.
- Seules les lignes satisfiant la condition seront sélectionnées.
- Possibilité d'utiliser les opérateurs de comparaison suivants :
	- `=` : test d'égalité
	- `<>` ou `!=` : test d'inégalité
	- `<`, `<=` : test strictement plus petit, plus petit ou égal
	- `>`, `>=` : test strictement plus grand, plus grand ou égal
- Les comparaisons peuvent être combinées avec les opérateurs logique `AND`, `OR` et `NOT`.

> *Cette clause ne doit pas obligatoirement être présente dans la requête `SELECT`*.


## Clause WHERE - Opérateur BETWEEN
- Opérateur de comparaison qui permet de tester si une valeur est entre deux autres valeurs.

Exemple : Sélectionner les personnes dont l'âge est entre 15 et 18 ans.

```sql
[...]
WHERE personne.age BETWEEN 15 AND 18
[...]
```

## Clause WHERE - Opérateur IN
- Opérateur de comparaison qui permet de tester si une valeur appartient à un ensemble de valeurs.

Exemple : Sélectionner les personnes qui ont 10 ou 20 ou 30 ou 40 ans.

```sql
[...]
WHERE personne.age IN (10, 20, 30, 40)
[...]
```

## Requête SELECT - Clause SELECT
- Spécifie les colonnes résultantes du produit cartésien qui seront sélectionnées dans la table résultante.
- Permet aussi d'agréger les données via les fonctions d'aggrégat.

Exemple : Afficher les colonnes `nom` et `prenom` de la table personne dans la table résultante.

```sql
SELECT personne.nom, personne,prenom
[...]
```

## Clause SELECT - \*
- L'étoile `*` permet de spécifier que le développeur ne souhaite pas décrire explicitement quelles colonnes sélectionner dans la table résultante.
- Les colonnes sélectionnées seront toutes celles présente dans la table au moment de l'exécution de la requête.
- Pratique dans certains cas mais à éviter en général car cela force le developpeur a connaître le schema des tables utilisées pour savoir quelles colonnes seront retournées.

## Clause SELECT - COUNT
- Compte le nombre de lignes dans la table résultante du produit cartésien (clause `FROM`) et du filtrage (clause `WHERE`).
- Agrège cette information dans une table contenant une seule ligne.
- Il est courant de passer `*` en paramètre de `COUNT`.

Exemple: Quel est le nombre de personnes ayant 18 ans ?

```sql
SELECT COUNT(*)
FROM personne
WHERE personne.age=18;
```

## Clause SELECT - MIN et MAX
- Retourne la valeur minimale ou maximale pour la colonne donnée en paramètre.
- Agrège cette information dans une table contenant une seule ligne.

Exemple : Quel est l'âge de la personne la plus jeune ?

```sql
SELECT MIN(personne.age)
FROM personne;
```

Exemple : Quel est l'âge de la personne la plus vieille ?

```sql
SELECT MAX(personne.age)
FROM personne;
```

## Clause SELECT - AVG
- Retourne la valeur moyenne pour la colonne donnée en paramètre.
- Agrège cette information dans une table contenant une seule ligne.

Exemple : Quel est l'âge des moyen des personnes ?

```sql
SELECT AVG(personne.age)
FROM personne;
```


## Exemple: SELECT
- Sélectionner le nom, le prénom et la préférence des personnes contenues dans la table personne.

```sql
SELECT personne.nom, personne.prenom, personne.preference
FROM personne;
```

- Sélectionner le nom des personnes ayant comme préférence le vin.

```sql
SELECT personne.nom
FROM personne
WHERE personne.preference = 'vin';
```

## Exercices
En utilisant le schéma de "Entreprise de fabrication et de distribution" :

produit(\underline{numP},libP,pu)

depot(\underline{numD})

stock(\underline{\#produit.numP,\#depot.numD},qtS,qtD)

client(\underline{numCl}, nom, prenom, ad, ca, red, \#depot.numD)

commande(\underline{numCo}, dateC, \#client.numCl, \#produit.numP, qtC)

## Exercices
Donnez les requêtes pour :

- Insérer le produit Bois à 10 euros / unité avec le numéro 10 dans la table `produit`.
- Changer le prix unitaire du Bois pour devenir 15e.
- Changer le prix unitaire du Bois pour devenir le quart de son prix actuel.
- Supprimer le produit Acier ayant comme numéro 3.
- Supprimer tous les produits ayant un prix inféreur à 10e.
- Lister le nom et prénom de tous les clients.
- Lister le nom des produits ayant un prix unitaire supérieur à 30e.
- Lister le nom et prénom des clients ayant un chiffre d'affaire supérieur à 15000 euros et comme prénom François.
- Compter le nombre de produit ayant un prix supérieur à 30e.
- Calculer la moyenne des prix des produits.
- Calculer le prix du produit le moins cher.
- Calculer le prix du produit le plus cher.

## Question plus difficile
Lister le nom des clients avec leurs numéros de commande.

La table résultante doit avoir le schéma suivant:

{ nom : TEXT, numCo : INTEGER }

## Avant de partir

Quels sont les deux types de requêtes SQL abordées dans ce cours et leurs usages ?
