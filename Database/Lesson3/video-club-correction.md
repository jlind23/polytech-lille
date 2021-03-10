## Videoclub

Pour la base de données stockant les données d'un vidéo-club ayant le schéma suivant :

abonne(\underline{nab}, nom, prenom)

dvd(\underline{ndvd}, anneeAchat, moisAchat, #film.nfilm)

emprunt(\underline{nemp}, datedeb, datefin, #abonne.nab, #dvd.ndvd)

categorie(\underline{ncat}, libelle)

film(\underline{nfilm}, titre, anneProduction, realisateur, #categorie.ncat)

Ecrire les requêtes SQL permettant d’obtenir les résultats suivants :

1. Tuples de la table ’film’
2. Titres des film parus entre 2005 et 2010, triés par ordre alphabétique.
3. Libellé des catégories dont font partie les films présents dans la base.
4. Noms et prénoms des abonnés ayant emprunté 'Pulp Fiction'.
5. Liste des films n’ayant jamais été empruntés.
6. Titre des films produits en 2008 ou 2009.
7. Liste des films dont au moins un dvd a été acheté l’année de sa production.
8. Titre des films réalisés ni en 2007, ni en 2008, ni en 2009.

```sql
-- 1.
SELECT film.nfilm, film.titre, film.anneProduction, film.categorie_ncat FROM film;
-- 2.
SELECT film.nfilm, film.titre, film.anneProduction, film.categorie_ncat
FROM film
WHERE anneeProduction >= 2005
  AND anneeProduction <= 2010;
-- 3.
SELECT film.nfilm, film.titre, film.anneProduction, film.categorie_ncat
FROM categorie
WHERE
  EXISTS (SELECT * FROM film WHERE film.ncat = categorie.ncat);
-- 4.
SELECT abonne.nomab, abonne.prenomab
FROM abonne, dvd, emprunt, film
WHERE abonne.nab = emprunt.nab
  AND emprunt.ndvd = dvd.ndvd
  AND dvd.nfilm = film.nfilm
  AND film.titre = 'Pulp Fiction';
-- 5.
SELECT *
FROM film
WHERE
  NOT EXISTS (SELECT *
              FROM emprunt, dvd
              WHERE emprunt.ndvd = dvd.ndvd
                AND dvd.nfilm = film.nfilm);
-- 6.
SELECT titre
FROM film
WHERE anneeProduction = 2008
  OR anneeProduction = 2009;
-- 7.
SELECT film.titre
FROM film
WHERE EXISTS (SELECT *
              FROM dvd
              WHERE dvd.nfilm = film.nfilm
              AND dvd.anneeachat = film.anneeProduction);
-- 8.
SELECT titre
FROM film
WHERE anneeProduction NOT IN (2007, 2008, 2009);

```