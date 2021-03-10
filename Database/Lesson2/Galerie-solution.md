# Gestion d’une galerie de peinture

## Contexte

On désire informatiser la gestion d’une galerie de peinture.
Toutes les oeuvres sont identifiées par un numéro, sont caractérisées par un titre, un genre (genres 'cubisme', 'impressionisme', 'pop-art',. . .) et sont réalisées par un ou plusieurs artistes.
Les informations à mémoriser pour un artiste sont son nom et sa date de naissance.
Dans la galerie peuvent se trouver plusieurs expositions. Chaque exposition est constituée de plusieurs salles qui sont parcourues dans un ordre précis. Certaines salles peuvent être partagées par plusieurs expositions. Chaque salle a un numéro unique et possède un nom. Une salle comporte plusieurs murs où sont exposées les différentes oeuvres.

## Exercice 1

Donnez les relations ainsi que les contraintes de clé primaire et de clé étrangère nécessaire pour implémenter cette base de données.

### Solution

oeuvre(\underline{numero}, titre, \#genre.nom)

genre(\underline{nom})

artiste(\underline{id}, nom, date\_naissance)

realisation(\underline{\#artiste.id, \#oeuvre.id})

exposition(\underline{id})

salle(\underline{numero}, nom)

parcours(\underline{\#exposition.id, \#salle.numero}, numero\_ordre)

mur(\underline{id}, \#salle.numéro, \#oeuvre.numero)


## Exercice 2

Donnez les commandes DDL qui permettent de créer cette base de données.

### Solution

```sql
CREATE TABLE genre(
	nom TEXT,
	PRIMARY KEY(nom)
);

CREATE TABLE oeuvre(
	numero INTEGER,
	titre TEXT,
	genre_cle INTEGER,
	PRIMARY KEY (numero),
	FOREIGN KEY (genre_cle) REFERENCES genre(nom)
);

CREATE TABLE artiste(
	id INTEGER,
	nom TEXT,
	date_naissance DATE,
	PRIMARY KEY (id)
);

CREATE TABLE realisation(
	artiste_id INTEGER,
	oeuvre_id INTEGER,
	PRIMARY KEY (artiste_id, oeuvre_id),
	FOREIGN KEY (artiste_id) REFERENCES artiste(id),
	FOREIGN KEY (oeuvre_id) REFERENCES oeuvre(id)
);

CREATE TABLE exposition(
	id INTEGER,
	PRIMARY KEY (id)
);

CREATE TABLE salle(
	numero INTEGER,
	nom TEXT,
	PRIMARY KEY (numero)
);

CREATE TABLE parcours(
	exposition_id INTEGER,
	salle_numero INTEGER,
	numero_ordre INTEGER,
	PRIMARY KEY (exposition_id, salle_numero),
	FOREIGN KEY (exposition_id) REFERENCES exposition(id),
	FOREIGN KEY (salle_numero) REFERENCES salle(numero)
);

CREATE TABLE mur(
	id INTEGER,
	salle_numero INTEGER,
	oeuvre_numero INTEGER,
	PRIMARY KEY (id),
	FOREIGN KEY (salle_numero) REFERENCES salle(numero),
	FOREIGN KEY (oeuvre_numero) REFERENCES oeuvre(numero)
);
```