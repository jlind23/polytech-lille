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