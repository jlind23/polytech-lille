# Chapitre 1 - Modèle relationnel 

## 1.1 Qu’est-ce qu’une donnée ? 

Ce cours porte sur SQL et les bases de données relationnelles. De ce fait, il est nécessaire de s’interroger sur ce que sont les données. Plusieurs défini tions existent dans la littérature. Dans le cadre de ce cours, nous utilisons la définition suivante. 

__Définition 1 (Données)__ Représentation conventionnelle d’une information en vue de son traitement informatique. - (Larousse, 2019) 
La façon de représenter conventionnellement la donnée va dépendre de la façon dont le concepteur du logiciel manipulant les données structure la don née. On distingue trois types de structurations : les données non structurées, les données semi-structurées et les données structurées. 

__Définition 2 (Données non-structurées)__ Données représentées ou sto ckées sans format prédéfini. 
Une photo, par exemple, contient des données non structurées. En effet, le sujet de la photo (e.g., une personne, un paysage, une voiture, etc...) n’est pas retrouvable via la structure du fichier contenant la photo. Déterminer les informations sémantiques présentes dans une photo est une tâche simple pour les humains. Il nous suffit de regarder quelques secondes une photo pour comprendre quel est son sujet. Pour un ordinateur, c’est une tâche complexe. 

__Définition 3 (Données semi-structurées)__ Forme de données structurées qui ne sont pas conformes à un modèle de données formel mais qui, néan moins, contiennent des tags permettant de distinguer des éléments séman tiques et créer une hiérarchie dans les données. 
Une page d’un site internet est créée à partir d’un fichier encodé dans un format de données semi-structurées : l’Hyper-Text Markup Language 
(HTML). Ce format est un compromis entre un traitement facile pour un ordinateur et la possibilité pour un humain de lire/comprendre les données facilement. 

__Définition 4 (Données structurées)__ Données disposées de façon à être traitées automatiquement et efficacement par un logiciel, mais pas nécessai rement par un humain. Ces données sont conformes à un modèle de données formel. 
Une base de données relationnelle contient des données structurées. C’est à dire que le format des données est entièrement décrit par la base de données et ne contient pas d’ambiguitées (en théorie). Dans le cadre de ce cours, nous allons nous intéresser à un type de base de données manipulant des données structurées. 

## 1.2 Historique rapide des modèles de données 

Peu de temps après que Alan Turing ait posé les bases de l’informatique moderne, un besoin de structurer et de stocker les données est apparu. La façon de structurer des données est décrite par le modèle de données utilisé. Ci-dessous se trouve un rapide historique des modèles de données. 
* Hiérarchique (60’) : Les données sont organisées sous la forme d’un arbre. Ce modèle dispose d’un langage de navigation dédié. 
* Réseau (fin 60’) : Les données sont organisées sous forme d’un graphe dirigé. Ce modèle dispose d’un langage de navigation dédié. 
* Relationnel (70’) : Données organisées sous forme de tables. Utilise SQL comme langage d’interrogation. Le programmeur n’a pas besoin de connaitre la structure "physique" des données pour les interroger. 
* Relationnel-objet (90’) : Extension du modèle relationnel avec les concepts venant de la programmation orientée objets. Fournit des types de données plus complexes. 
* Orienté-objet (fin 90’) : Offre directement une persistance aux ins tances objets. 
* NoSQL (début 2010) : Modèle emmergant permettant la manipula tion de d’importants volumes de données. Ces systèmes ne respectent dn général pas les standards du modèle relationnel. Cette propriété est issue d’une concession permettant des traitements plus rapides pour certains types d’applications. 

Dans le cadre de ce cours, nous allons nous intéresser au modèle rela tionnel. Un aspect intéressant de ce modèle de données est qu’il repose sur des bases mathématiques solides affinées depuis plusieurs décennies par la communauté scientifique. 
Malgré les avancées dans la recherche en base de données, les bases de données relationnelles restent largement utilisées dans l’industrie. De nom breux systèmes de gestions de bases de données relationnelles existent et sont toujours activement développés (e.g., MariaDB, MySQL, Oracle, Post greSQL, ...). 

## 1.3 Découverte du modèle relationnel 

Cette activité a pour but de vous familiariser avec les concepts du modèle relationel. Elle peut être effectuée seul ou par groupe de deux personnes. 

### 1.3.1 Contexte 

Un e-mail a été envoyé à 15 de vos contacts afin de connaitre leur boisson préférée dans le but d’organiser une soirée entre amis. 


| De : julien |
| ----- |
| À : timothee.lafontaine, arlette.beland, anais.pichette, [...] Sujet : Donnez moi vos préférences en boissons ! |
| Bonjour les amis, Dans le cadre de la soirée de la semaine prochaine, j’aimerais connaître votre boisson préférée. Pouvez-vous, s’il vous plait, structurer votre réponse comme suit : Ma boisson préférée est : XXX Un grand merci d’avance. Julien |


Les réponses à ce mail sont disponibles en annexe A. 

### 1.3.2 Structurons les données 

Afin d’y voir un peu plus clair dans les réponses de nos invités, nous voulons stocker leurs préférences dans un tableau. Pour se faire, lisez les
mails des invités et créez un tableau qui regroupe les informations suivantes : prénom, nom, préférence. La préférence est le nom de la boisson préférée de l’invité. 

| Nom | Prénom | Préférence |
| --- | --- | --- |
| ... | ... | ... |
| ... | ... | ... |
| ... | ... | ... |
| ... | ... | ... |

Table 1.1 – Tableau attendu pour stocker les données. 

### 1.3.3 Coût de la soirée 

Maintenant que nous avons un aperçu des préférences des invités, nous voulons estimer le coût total de la soirée. Pour se faire, il serait judicieux de stocker le prix unitaire de chacune de ces boissons. Ajoutez une colonne à votre tableau afin de stocker cette nouvelle information. 
— Le prix unitaire d’un cola est de 1.5e ; 
— Le prix unitaire d’une bière est de 2e ; 
— Le prix unitaire d’un verre de vin est de 2e et ; 
— Le prix unitaire d’une limonade est de 1.5e. 

| Nom | Prénom | Préférence | Prix unitaire |
| --- | --- | --- | --- |
| ... | ... | ... | ... |
| ... | ... | ... | ... |
| ... | ... | ... | ... |
| ... | ... | ... | ... |

Table 1.2 – Nouveau tableau attendu pour stocker les données. 

### 1.3.4 Une erreur fortuite 

Malheureusement, une erreur s’est glissée dans la consigne précédente. Le prix unitaire d’un verre de limonade est erroné. En réalité, un verre de limonade coûte 1,7e. Mettez à jour le tableau afin de prendre en compte cette information. 
— Qu’est-ce qui est génant dans la mise à jour de cette infor mation ? 
— Que peut-on faire pour palier à ce problème ?

### 1.3.5 Vers une meilleure structuration 

Selon nos observations lors de l’étape précédente, la structuration des données n’est pas optimale. En effet, mettre à jour le prix d’une boisson est fastidieux. Restructurez les données en deux tables : personne et boisson. 
— Qu’implique l’utilisation d’une table auxilliaire pour stocker les boissons préférées sur les données de la table boisson ? 
— Et sur les données de la table personne ? 

## 1.4 Le modèle relationnel 

Maintenant que nous avons une intuition concernant ce qu’est une base de données relationelle, il est temps de définir explicitement chaque concept. 

### 1.4.1 Base de données d’exemple 

Pour la suite de ce chapitre, la base de données ci-dessous (Table 1.3 et Table 1.4) sera utilisée comme exemple principal. 
Id 
Nom 
Prénom 
#boisson.Id








1 
2 
3 
4 
5 
6 
7 
8 
9 
10 
11 
12 
13 
14 
15 
‘Timothée’ ‘Arlette’ 
‘Anaïs’ 
‘Éric’ 
‘Bruno’ 
‘Felicienne’ ‘Simone’ 
‘Hamilton’ 
‘Yvette’ 
‘Théophile’ ‘Hugues’ 
‘Florence’ 
‘Hilaire’ 
‘Suzette’ 
‘Louis’ 
‘Lafontaine’ ‘Béland’ 
‘Pichette’ 
‘Ratté’ 
‘Aubé’ 
‘Cloutier’ 
‘Bourget’ 
‘Camus’ 
‘Bérard’ 
‘Allain’ 
‘Laisné’ 
‘Verreau’ 
‘Ouellet’ 
‘Lampron’ 
‘Déziel’ 
3 
4 
2 
1 
4 
1 
1 
1 
2 
4 
1 
4 
1 
3 
4


Table 1.3 – Table personne. 
1.4.2 Les concepts du modèle relationnel 
Le modèle relationnel est construit à partir de 8 concepts. Dans cette sec tion, nous allons poser les définitions de ces concepts et les illustrer concrê-
Id 
Dénomination 
Prix unitaire






1 
2 
3 
4 
‘limonade’ 
‘bière’ 
‘cola’ 
‘vin’ 
1,70 
2,00 
1,50 
2,00


Table 1.4 – Table boisson. 
tement. 
Définition 5 (Attribut) Colonne nommée d’une table. Le nom de chaque attribut dans une relation est unique au sein de celle-ci. Chaque attribut est mono-valué, c’est à dire qu’il ne peut contenir qu’une valeur atomique et pas une collection de valeurs. 
Dans la base de données d’exemple, Nom est un attribut de la table personne. 
Quels sont les autres attributs des tables personne et boisson ? 
Définition 6 (Domaine) Ensemble de valeurs caractérisées par un nom. Similaire au type d’une variable dans un langage de programmation. 
Par exemple, le domaine MONEY représente des nombres à deux dé cimales, il est utilisé pour les calculs concernant l’argent (1.05, 200.00, -18.45, etc... mais pas ‘Jean’, 3.1415, etc...). 
Un autre exemple est le domaine DATE qui représente les dates du ca lendrier. (e.g. 25/12/2018, etc... mais pas 1.05, ‘Jean’, etc...) 
Quel est le domaine de la colonne prix unitaire dans la base de données d’exemple ? 
Définition 7 (Schéma de relation) Ensemble d’attributs avec, pour chaque attribut, un domaine qui lui est associé. 
Par exemple, dans la base de données d’exemple, le schéma de la table boisson est : { Id : INTEGER, Dénomination : TEXT, Prix Unitaire : MONEY } 
Quel est le schéma de la table personne de l’activité précédente ?
1.4. LE MODÈLE RELATIONNEL 13 
Définition 8 (Tuple) Ensemble d’attributs associés aux valeurs apparte nant à leurs domaines respectifs. Aussi appelé “ligne” ou “row” en anglais. 
Pour le schéma de la table boisson, le tuple suivant est possible : { Id : 1, Dénomination : ‘limonade’, Prix Unitaire : 1,70 } 
Pouvez-vous donner un tuple de la table personne ? 
Définition 9 (Relation) Il s’agit d’un schéma de relation et d’un ensemble de tuples associés à un nom. Aussi appelé “table”. 
Dans la base de données d’exemple, la relation boisson est définie par : 
1. Le schéma de relation 
{ Id : INTEGER, Dénomination : TEXT, Prix Unitaire : MONEY } 
2. L’ensemble de tuples : 
{ 
{ Id : 1, prenom : ‘limonade’, Prix Unitaire : 1,70 }, { Id : 2, prenom : ‘bière’, Prix Unitaire : 2,00 }, { Id : 3, prenom : ‘cola’, Prix Unitaire : 1,50 }, { Id : 4, prenom : ‘vin’, Prix Unitaire : 2,00 } 
} 
Dans le cadre de ce cours nous utilisons la convention suivante pour référer à une table : nom_de_la_table(attributs). Par exemple, pour la table boisson : boisson(Id,Dénomination,Prix Unitaire). 
Pouvez-vous donner le schéma et l’ensemble des tuples de la table personne ? 
Définition 10 (Contrainte d’intégrité) Assertion vérifiée par les don nées de la base à tout moment. L’objectif des contraintes d’intégrité est d’as surer la cohérence logique de la base de données. 
Définition 11 (Clé primaire) Contrainte portant sur une relation. Im pose l’unicité des valeurs d’un groupe d’attributs (la clé). 
— La contrainte de clé primaire permet de s’assurer que chaque ligne est identifiable de façon unique dans la table. 
— Par convention, les attributs concernés par la contrainte de clé pri maire seront soulignés dans le schéma de relation.
Serait-il judicieux de choisir le couple de colonnes (Nom, Prénom) comme clé primaire de la table personne ? Pourquoi ? Quelle autre information relative à une personne (absente de la table en l’état) pourrait être utilisée comme clé primaire ? 
Quel(s) attribut(s) de la table boisson ont une contrainte de clé primaire ? Justifiez votre réponse. 
En général, pour chaque table, on utilise une colonne nommée Id de type INTEGER comme clé primaire. 
En extension de la convention de notation décrite précédemment, on spécifie qu’un ou plusieurs attributs sont soumis à une clé primaire en les soulignant. Par exemple, pour la table boisson, Id est souligné : boisson(Id,Dénomination,Prix Unitaire). 
Définition 12 (Clé étrangère) Contrainte portant sur une relation R1 qui consiste à specifier que les valeurs d’un groupe d’attributs sont un sous ensemble des valeurs du groupe d’attributs relatif à la clé primaire d’une relation R2. 
— Les valeurs des attributs de la clé étrangère dans un tuple de R1 ap paraissent donc comme valeurs des attributs de la clé primaire de R2. — Une table peut avoir plusieurs clés étrangères. 
— Par convention, on spécifie les clés étrangères en les préfixant par # : R2(att1,att2,...) 
R1(att1,att2,#R2.att1,...) 
Reprenons le schéma de relation personne : { id: INTEGER, nom : TEXT, prenom : TEXT, age : INTEGER } et imaginons que nous voulons stocker la ville d’origine de la personne. Cette ville est stockée dans une table ville ayant le schéma de relation suivant : { id: INTEGER, nom : TEXT } 
Il est possible de lier une personne à sa ville d’origine en deux étapes : 1. Ajouter un attribut ville.id au schéma de relation personne. 2. Ajouter une clé étrangère sur le groupe d’attributs composé de (ville.id) 
de la table personne qui fait référence à la clé primaire de la table ville. 
La clé étrangère sera alors exprimée comme suit : 
ville(id, nom) 
personne(id,nom,prenom,age,#ville.id) 
Dans la base de données d’exemple, quelle est la contrainte de clé étrangère entre personne et boisson ?
1.4. LE MODÈLE RELATIONNEL 15 
1.4.3 Relation n-m 
On souhaite ajouter une table plat qui contient les plats qui ont déjà été servis à des personnes. Pour chaque plat, cette table stock le nom de celui-ci. plat(nom) 
On souhaite stocker les plats consommés par chaque personne et leurs dates de consommation. 
Nous pouvons observer que : 
— Un plat peut avoir été consommé par plusieurs personnes (n per sonnes). 
— Une personne peut avoir consommé plusieurs plats (m plats). 
Quelle(s) modification(s) apporter au schéma relationel pour sto cker la relation entre plat et personne ?
