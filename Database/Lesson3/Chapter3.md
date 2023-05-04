
## Avant de commencer

Quels sont les deux types requêtes SQL abordées dans ce cours et leurs usages ?

## En résumé
Structured Query Language, le langage de requêtes structuré.

- Data Definition Language (DDL)
	- CREATE TABLE - Créer une table et spécifier la clé primaire et les clés étrangères.
	- DROP TABLE - Supprimer une table.
- Data Manipulation Language (DML)
	- INSERT - Insérer des données.
	- UPDATE - Mettre à jour des données.
	- DELETE - Supprimer des données.
	- SELECT - Lire des données.

## Requête SELECT - Ordonner les données

- La clause `ORDER BY` permet d'ordonner les tuples résultants de la requête selon les valeurs d'un ou plusieurs attributs.
- Le mot clé `ASC` ordonne les tuples par ordre croissant et `DESC` par ordre décroissant.

```sql
[...]
ORDER BY column1 [ASC | DESC], column1 [ASC | DESC], ...
[...]
```

Exemple: Ordonner les personnes par nom de familles puis par prénom si deux noms de famille sont identiques.

```sql
SELECT personne.nom personne.prenom
FROM personne
ORDER BY personne.nom ASC, personne.prenom ASC;
```

## Requête SELECT - Limiter le nombre de tuples

- La clause `LIMIT` permet de spécifier le nombre de tuples que l'on souhaite obtenir en résultat.
- Les `n` premiers tuples seront conservés et les autres ignorés (et perdus!).
- À utiliser avec la clause `ORDER BY` car sans celle-ci on ne peut pas faire d'hypothèse sur l'ordre des tuples.

```sql
[...]
LIMIT <n>
[...]
```

Exemple: Ordonner les personnes par nom de familles puis par prénom si deux noms de famille sont identiques et ne garder que les 5 premières.

```sql
SELECT personne.nom personne.prenom
FROM personne
ORDER BY personne.nom ASC, personne.prenom ASC
LIMIT 5;
```

# Jointure de tables

## Jointure de tables
Les jointures de tables en SQL permettent d'associer des lignes de deux tables via l’égalité des valeurs d’une colonne d’une première table par rapport à la valeur d’une colonne d’une seconde table.

La jointure entre deux tables est calculée en filtrant les lignes résultantes du produit cartésien entre les deux tables.

## Jointure de tables, en pratique
La jointure se fait dans la clause `WHERE` de la requête `SELECT`.

```sql
SELECT [...]
FROM table1, table2
WHERE table1.column1 = table2.column2;
```

## Jointure - Exemple 1
Sélectionner le prénom de chaque personne et le prix unitaire de la boisson qu'ils préfèrent.

```sql
SELECT personne.prenom, boisson.prix_unitaire
FROM personne, boisson
WHERE personne.preference = boisson.denomination;
```


## Jointure - Exemple 2
Sélectionner le nom de chaque personne dont la boisson préférée coûte plus de 1,5 euro:

```sql
SELECT personne.nom
FROM personne, boisson
WHERE personne.preference = boisson.denomination
	AND boisson.prix > 1.5;
```


## Jointure de tables : Remarque
Quand **n tables** sont présentes dans la clause `FROM` d'une requête `SELECT`, il faut au minimum **n-1 jointures** séparées par des `AND`.

Voyez-vous pourquoi?

## Exercice :
En utilisant le schéma de "Entreprise de fabrication et de distribution" :

produit(\underline{numP},libP,pu)

depot(\underline{numD})

stock(\underline{\#numP,\#numD},qtS,qtD)

client(\underline{numCl}, nom, prenom, ad, ca, red, \#numD)

commande(\underline{numCo}, dateC, \#numCl, \#numP, qtC)

Donnez une requête qui retourne pour chaque commande : son numéro, sa date, le nom, le prénom du client associé et le libellé du produit commandé.

# Opération ensemblistes

## Union de requêtes SELECT
Effectue l'union des tuples résultants de deux requêtes `SELECT`.

```sql
<select1>
UNION
<select2>;
```

Attention : Les tables résultantes de `<select1>` et `<select2>` doivent avoir le même schéma.

## Union de requêtes SELECT : Exemple

Quels sont les noms et prénoms des personnes ayant comme préférence le vin ou la bière ?

```sql
SELECT personne.nom, personne.prenom
FROM personne
WHERE preference = 'Vin'
UNION
SELECT personne.nom, personne.prenom
FROM personne
WHERE preference = 'Biere';
```

## Intersection de requêtes SELECT
Effectue l'intersection des tuples résultants de deux requêtes `SELECT`.

```sql
<select1>
INTERSECT
<select2>;
```

Attention : Les tables résultantes de `<select1>` et `<select2>` doivent avoir le même schéma.

## Intersection de requêtes SELECT : Exemple

Quels sont les clients dont le chiffre d'affaire est compris entre 1000 et 5000e ?

```sql
SELECT client.nom, client.prenom
FROM client
WHERE client.ca >= 1000
INTERSECT
SELECT client.nom, client.prenom
FROM client
WHERE client.ca <= 5000;
```

## Différence de requêtes SELECT
Effectue la différence des tuples résultants de deux requêtes `SELECT`.

```sql
<select1>
EXCEPT
<select2>;
```

Attention : Les tables résultantes de `<select1>` et `<select2>` doivent avoir le même schéma.

## Différence de requêtes SELECT : Exemple
Quels sont les clients dont le chiffre d'affaire est supérieur à 1000 euros mais dont le chiffre d'affaire n'est pas de 1500 euros?

```sql
SELECT client.nom, client.prenom
FROM client
WHERE client.ca >= 1000
EXCEPT
SELECT client.nom, client.prenom
FROM client
WHERE client.ca = 1500;
```

# Sous-requête

## Sous-requête
- SQL permet d'exécuter des sous-requêtes.
- Il s'agit de requêtes `SELECT` qui se trouvent à l'intérieur d'une autre requête `SELECT`.
- Une sous-requête fournit des données à la requête qui la contient.
- Une sous-requête peut retourne un ou plusieurs tuples.
- Une sous-requête doit être entourée de parenthèses.

## Sous-requête - Forme 1

```sql
SELECT <table1.c1>
FROM <table>
WHERE <table1.c2> IN (SELECT <table2.c1>
						FROM <table2>
						WHERE <condition>);
```

## Sous-requête - Forme 1 : Exemple
En utilisant le schéma de "Entreprise de fabrication et de distribution".

Quels sont les libellés des produits pour lesquels il existe une commande de quantité 100 ?

```sql
SELECT produit.libP
FROM produit
WHERE produit.numP IN (SELECT commande.produit_numP
							FROM commande
							WHERE commande.qtC = 100);
```

## Sous-requête - Forme 2


```sql
SELECT <table1.c1>
FROM <table>
WHERE EXISTS (SELECT <table2.c1>
				 FROM <table2>
				 WHERE <condition>);
```

## Sous-requête - Forme 2 : Exemple

Quels sont les libellés des produits pour lesquels il existe une commande de quantité supérieure à 100 ?

```sql
SELECT produit.libP
FROM produit
WHERE EXISTS 
	(SELECT *
	 FROM commande
	 WHERE commande.produit_numP = produit.numP
		AND commande.qtC > 100);
```

## Sous-requête - Forme 3

```sql
SELECT 
	<table1.c1>, 
	(SELECT <table2.c1>
	 FROM table2
	 WHERE <condition>) AS 'Nom de la column'
FROM <table>;
[...]
```
## Sous-requête - Forme 3 : Exemple
En utilisant le schéma de "Entreprise de fabrication et de distribution".

Lister les clients et, pour chaque client, le nombre de commandes qui les concernent.

```sql
SELECT
	client.nom,
	client.prenom,
	(SELECT COUNT(*)
	 FROM commande
	 WHERE commande.client_numCl = client.numCl
	) AS 'Nombre de commandes'
FROM client;
```

# L'absence d'information

## L'absence d'information

Comment représenter une information inconnue dans la base de données ?

Exemple : Dans la table personne, vous souhaitez stocker l'âge des personnes seulement si elles sont d'accord.

## NULL
- La valeur `NULL` permet de représenter une information manquante.
- Elle est sémantiquement différente de la valeur 0 ou d'un `TEXT` vide.

## Particularités
- `NULL = NULL` - Retourne la valeur `NULL`.
- `NULL <> NULL` - Retourne la valeur `NULL`.
- `1 + NULL` - Retourne la valeur `NULL`.
- `TRUE AND NULL` - Retourne la valeur `NULL`.
- `TRUE OR NULL` - Retourne la valeur `TRUE`.
- `FALSE AND NULL` - REtourne la valeur `FALSE`.
- `FALSE OR NULL` - Retourne la valeur `NULL`.

## Prédicats de test

- `<x> IS NULL` - Retourne `TRUE` si `x` est `NULL`.
- `IS NOT NULL` - Retourne `FALSE` si `x` est `NULL`.
