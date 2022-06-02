# À ajouter dans le Bashrc de votre compte
export PGHOST=serveur-etu.polytech-lille.fr                       (à placer dans ~/.bashrc)

# Creation d'une base de donnée
createdb dbname -U username
  
# Suppression de la base
dropdb dbname -U username

# Connexion à la base
psql dbname -U username

# Correction exercice DDL - "Entreprise de fabrication et de distribution"
```sql
CREATE TABLE produit(
  numP INTEGER,
  libP TEXT,
  pu MONEY,
  PRIMARY KEY (numP)
);
CREATE TABLE depot(
  numD INTEGER,
  PRIMARY KEY (numD)
);
CREATE TABLE stock(
  produit_numP INTEGER,
  depot_numD INTEGER,
  qtS INTEGER,
  qtD INTEGER,
  PRIMARY KEY (produit_numP, depot_numD),
  FOREIGN KEY (produit_numP) REFERENCES produit(numP),
  FOREIGN KEY (depot_numD) REFERENCES depot(numD)
);
CREATE TABLE client (
  numCl INTEGER,
  nom TEXT,
  prenom TEXT,
  ad TEXT,
  ca MONEY,
  red DOUBLE,
  depot_pref INTEGER,
  PRIMARY KEY (numCl),
  FOREIGN KEY (depot_pref) REFERENCES depot(numD)
);
CREATE TABLE commande(
  numCo INTEGER,
  dateC DATE,
  client_numCl INTEGER,
  produit_numP INTEGER,
  qtC INTEGER,
  PRIMARY KEY (numCo),
  FOREIGN KEY (client_numCl) REFERENCES client(numCl),
  FOREIGN KEY (produit_numP) REFERENCES produit(numP)
);


Solution

INSERT INTO produit(numP,libP,pu)
VALUES (10,'Bois',10);

UPDATE produit
SET pu='15'
where libP='Bois';

UPDATE produit
SET pu=pu*0.25
where libP='Bois';

DETELE FROM Produit
WHERE numP=3;

DELETE FROM Produit
WHERE pu <10;

SELECT nom, prenom
FROM client;

SELECT libP
FROM produit
where pu >30;

SELECT nom, prenom 
FROM Client
WHERE client.nom='françois' and ca > 15 000;


```
