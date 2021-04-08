# À ajouter dans le Bashrc de votre compte
export PGHOST=serveur-etu.polytech-lille.fr                       (à placer dans ~/.bashrc)

# Creation d'une base de donnée
createdb <dbname> -U <username>
  
# Suppression de la base
dropdb <dbname> -U <username>

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
```
