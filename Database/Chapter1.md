
# _Modèle relationnel_

# Qu'est-ce qu'une donnée ?

## Définitions
Plusieurs définitions. En particulier (Larousse, 2019) :

> "Résultats d'observations ou d'expériences faites délibérément ou à l'occasion d'autres tâches et soumis aux méthodes statistiques."

> "Représentation conventionnelle d'une information en vue de son traitement informatique."

## Structuration des données
- **Données non-structurée** - Données représentées ou stockées sans format prédéfini.
- **Données structurée** - Données  disposées de façon à être traitées automatiquement et efficacement par un logiciel, mais pas nécessairement par un humain. Ces données sont conformes à un modèle de données formel.
- **Données semi-structurée** - Forme de données structurées qui ne sont pas conformes à un modèle de données formel mais qui, néanmoins, contiennent des tags permettant de distinguer des éléments sémantiques et créer une hiérarchie dans les données.

## Historique rapide des modèles de données
- **Hiérarchique** (60') : Données organisées sous la forme d'un arbre et dispose d'un langage de navigation dédié.
- **Réseau** (fin 60') : Données organisées sous forme d'un graphe dirigé et dispose d'un langage de navigation dédié.
- **Relationnel** (70') : Données organisées sous forme de tables. Utilise SQL comme langage d'interrogation. Le programmeur n'a **pas** besoin de connaître la structure "physique" des données pour les interroger.

**Modèle étudié dans le cadre de ce cours !**

- **Relationnel-objet** (90') : Extension du modèle relationnel avec les concepts venant de la programmation orienté objets. Types de données plus complexe, etc.
- **Orienté-objet** (fin 90') : Offre directement une persistance aux instances objets.

[//]: # Source: https://www.fing.edu.uy/inco/grupos/csi/esp/Cursos/cursos_act/2000/DAP_DisAvDB/documentacion/OO/Evol_DataModels.html

# Activité

## Contexte
Un mail a été envoyé à 15 de vos contacts afin de connaître leur boisson préférée dans le but d'organiser une soirée entre amis.

## Le mail

> *De:* julien
>
> *À:* timothee.lafontaine, arlette.beland, anais.pichette, [...]
>
> *Sujet:* Donnez moi vos préférences en boissons !
>
> Bonjour les amis,
>
> Dans le cadre de la soirée de la semaine prochaine j'aimerais connaître votre boisson préférée.
>
> Pouvez-vous, s'il vous plait, structurer votre réponse comme suit :
>
> Ma boisson préférée est: XXX
>
> Un grand merci d'avance.
>
> Julien
>

## Exercice 1

Afin d'y voir un peu plus clair dans les réponses de nos invités, nous voulons stocker leurs préférences dans un tableau. Pour se faire, lisez les mails des invités et créez un tableau qui regroupe les informations suivantes : prénom, nom, préférence. La préférence étant le nom de la boisson préférée de l'invité.

| Nom | Prénom | Préférence |
|:---:|:------:|:----------:|
| ... |  ...   | ...        |
| ... |  ...   | ...        |
| ... |  ...   | ...        |
| ... |  ...   | ...        |

## Exercice 2

De plus, nous voudrions stocker dans cette table le **prix unitaire** de chacune de ces boissons.

- Ajoutez une colonne à votre tableau afin de stocker celui-ci.
	+ Le prix unitaire d'un cola est de 1.5e ;
	+ celui d'une bière est de 2e ;
	+ celui d'un verre de vin est de 2e et ;
	+ celui d'une limonade est de 1.5e.

| Nom | Prénom | Préférence | Prix unitaire |
|:---:|:------:|:----------:|:-------------:|
| ... |  ...   | ...        | ...           |
| ... |  ...   | ...        | ...           |
| ... |  ...   | ...        | ...           |
| ... |  ...   | ...        | ...           |

## Exercice 3

Oups, malheureusement, une erreur s'est glissée dans la consigne précédente. Le prix unitaire d'un verre de limonade est erroné. En réalité, un verre de limonade coûte 1.7e.

- Mettez à jour le tableau afin de prendre en compte cette information.
- Qu'est-ce qui est gênant dans la mise à jour de cette information ?
- Que peut-on faire pour palier à ce problème ?

## Exercice 4

Restructurez les données en deux tables : *personne* et *boisson*.

- Qu'implique l'utilisation d'une table auxiliaire pour stocker les boissons préférées sur les données de la table *boisson* ?
- Et sur les données de la table *personne* ?

# Le modèle relationnel

## Attribut

### Définition :
Colonne nommée d'une table. Le nom de chaque attribut dans une relation est unique au sein de cette relation.

Chaque attribut est mono-valué, c'est à dire qu'il ne peut contenir qu'une valeur atomique et pas une collection de valeurs.

### Exemple :
- Nom est un attribut de la table personne vue précédemment.

### Question :
- Quels sont les autres attributs des tables `personne` et `boisson` ?

| Nom | Prénom | Préférence |
|:---:|:------:|:----------:|

| Dénomination | Prix unitaire |
|:------------:|:-------------:|

## Domaine
### Définition :
Ensemble de valeurs caractérisées par un nom. Similaire au type d'une variable dans un langage de programmation.

### Exemples :
+ Le domaine MONEY représente des nombres à deux décimales, il est utilisé pour les calculs concernant l'argent (`1.05`, `200.00`, `-18.45`, etc... mais pas "Jean", `3.1415`, etc...)
+ Le domaine DATE représente les dates du calendrier. (e.g. `25/12/2018`, etc... mais pas `1.05`, `"Jean"`, etc...)

### Questions :

+ Quel est le domaine de la colonne `prix unitaire` dans l'activité précédente ?

| Dénomination | Prix unitaire |
|:------------:|:-------------:|

## Schéma de relation

### Définition :
Ensemble d'attributs avec, pour chaque attribut, un domaine qui lui est associé.

### Exemple :

```
{ nom : TEXT, prenom : TEXT, age : INTEGER }
```

### Question :
Quel est le schéma de la table `boisson` de l'activité précédente ?

| Dénomination | Prix unitaire |
|:------------:|:-------------:|

## Tuple
### Définition :
Ensemble d’attributs associés aux valeurs appartenant à leurs domaines respectifs.
Parfois aussi appelé "ligne" ou "row" en anglais.

### Exemple :
Pour le schéma de relation précédent, le tuple suivant est possible : { nom : "lind", prenom : "Julien", age: 24 }

### Question :
Pouvez-vous me donner un tuple de l'une des tables de l'activité précédente ?

## Relation (ou Table)

### Définition :
Il s'agit d'un schéma de relation et d'un ensemble de tuples associés à un nom.

### Exemple :
La relation `personne` est définie par :

+ Le schéma de relation { nom : TEXT, prenom : TEXT, age : INTEGER }
+ L'ensemble de tuples:

 ```
{
{ nom : "lind", prenom : "Julien", age : 24 },
{ nom : "Larcheveque", prenom : "Guillaume", age : 33 },
{ nom : "Ferlicot", prenom : "Cyril", age : 25 }
}
 ```
 
+ Dans le cadre de ce cours nous utilisons la convention suivante : `personne(nom,prenom,age)`

## Contrainte d'intégrité
### Objectif :
Assurer la cohérence logique de la base de données.

### Définition :
Assertion vérifiée par les données de la base à tout moment.

## Clé primaire

### Définition :
Contrainte portant sur une relation. Impose l'unicité des valeurs d'un groupe d'attributs (la clé).

- La contrainte de clé primaire permet de s'assurer que chaque ligne est identifiable de façon unique dans la table.
- Par convention, les attributs concernés par la contrainte de clé primaire seront soulignés dans le schéma de relation.

## Exemple (clé primaire)
Pour la relation précédente `personne`, s'il n'existe pas 2 personnes ayant le même couple (`nom`,`prenom`), on peut définir une clé primaire sur le groupe d'attribut (`nom`, `prenom`).

# Le schéma de relation est alors noté { <ins>nom : TEXT</ins>, <ins>prenom : TEXT</ins>, age : INTEGER }.

## Questions (clé primaire)
- Pour la relation `personne`, quelle information (absente de la table en l'état) pourrait être utilisée comme clé primaire ?
- Dans l'activité précédente, quel(s) attribut(s) de quelles tables ont une contrainte de clé primaire ?

## Remarque (clé primaire)
En général, on utilise une colonne nommée `id` de type `INTEGER` comme clé primaire pour toutes les tables.

Exemple : personne(<ins>id</ins>, nom, prenom, age)

## Clé étrangère

### Définition :
Contrainte portant sur une relation R1 qui consiste à specifier que les valeurs d'un groupe d'attributs sont *un sous ensemble* des valeurs du groupe d'attributs relatif à la clé primaire d'une relation R2.

- Les valeurs des attributs de la clé étrangère dans un tuple de R1 apparaissent donc comme valeurs des attributs de la clé primaire de R2.
- Une table *peut* avoir *plusieurs* clés étrangères.
- Par convention, on spécifie les clés étrangères en les préfixant par \# :

R2(<ins>att1</ins>,att2,...)

R1(att1,att2,#R2.att1,...)


## Exemple (clé étrangère)
Reprenons le schéma de relation personne : { _id: INTEGER_, nom : TEXT, prenom : TEXT, age : INTEGER } et imaginons que nous voulons maintenant stocker la ville d'origine de la personne. Cette ville est stockée dans une table `ville` ayant le schéma de relation suivant : { \underline{id: INTEGER}, nom : TEXT }.

Il est possible de lier une personne à sa ville d'origine en deux étapes:

1. Ajouter un attribut `ville.id` au schéma de relation `personne`.
2. Ajouter une clé étrangère sur le groupe d'attributs composé de (`ville.id`) de la table `personne` qui référence la clé primaire de la table `ville`.

La clé étrangère sera alors exprimée comme suit :

ville(<ins>id</ins>, nom)

personne(<ins>id</ins>,nom,prenom,age,#ville.id)

## Question (clé étrangère)

Dans l'activité précédente, y a t-il une contrainte de clé étrangère ?

| Nom | Prénom | Préférence |
|:---:|:------:|:----------:|

| Dénomination | Prix unitaire |
|:------------:|:-------------:|

## Relation n-m

On souhaite ajouter une table `plat` qui contient les plats qui ont déjà été servis à des personnes. Pour chaque plat, cette table stocke le nom de celui-ci.

plat(<ins>nom</ins>)

On souhaite stocker l'information concernant le fait qu'une personne ait consommé un plat et la date à laquelle cette consommation a eu lieu.

Question : comment stocker l'association plat-personne?

## Relation n-m : Observations
- Un plat peut avoir été consommé par plusieurs personnes (`n` personnes)
- Une personne peut avoir consommé plusieurs plats (`m` plats)

## Relation n-m : Solution
- Utiliser une table intermédiaire pour stocker la consommation d'un plat par une personne :

consommation(<ins>id</ins>, #personne.id,#plat.nom, date)

## Exercice 5
Voir feuille "Entreprise de fabrication et de distribution"

## Avant de partir
Quels sont les concepts de base du modèle relationnel ?
