# Activité 1 : Préférences en boissons

## Exercice 1.
> Afin d'y voir un peu plus clair dans les réponses de nos invités, nous voulons stocker leurs préférences dans un tableau. Pour ce faire, lisez les mails des invités et créez un tableau qui regroupe les informations suivantes: prénom, nom, préférence. La préférence étant le nom de la boisson préférée de l'invité.

|*Personne*| Prénom | Nom | Préférence |
|:------:|:------:|:---:|:----------:|
|| Timothée | Lafontaine | cola |
|| Arlette | Béland | vin |
|| Anaïs | Pichette | bière |
|| Éric | Ratté | limonade |
|| Bruno | Aubé | vin |
|| Felicienne | Cloutier | limonade |
|| Simone | Bourget | limonade |
|| Hamilton | Camus | limonade |
|| Yvette | Bérard | bière |
|| Théophile | Allain | vin |
|| Hugues | Laisné | limonade |
|| Florence | Verreau | vin |
|| Hilaire | Ouellet | limonade |
|| Suzette | Lampron | cola |
|| Louis | Déziel | vin |

## Exercice 2.
> De plus, nous voudrions stocker dans cette table le **prix unitaire** de chacune de ces boisson. Ajouter une colonne à votre tableau afin de stocker celui-ci. Le prix unitaire d'un cola est de 1.5e, celui d'une bière est de 2e, celui d'un verre de vin est de 2e et celui d'une limonade est de 1.5e.

|*Personne*| Prénom | Nom | Préférence | Prix |
|:------:|:------:|:---:|:----------:|:----:|
|| Timothée | Lafontaine | cola | 1.5 |
|| Arlette | Béland | vin | 2 |
|| Anaïs | Pichette | bière | 2 |
|| Éric | Ratté | limonade | 1.5 |
|| Bruno | Aubé | vin | 2 |
|| Felicienne | Cloutier | limonade | 1.5 |
|| Simone | Bourget | limonade | 1.5 |
|| Hamilton | Camus | limonade | 1.5 |
|| Yvette | Bérard | bière | 2 |
|| Théophile | Allain | vin | 2 |
|| Hugues | Laisné | limonade | 1.5 |
|| Florence | Verreau | vin | 2 |
|| Hilaire | Ouellet | limonade | 1.5 |
|| Suzette | Lampron | cola | 1.5 |
|| Louis | Déziel | vin | 2 |

## Exercice 3.
> Oups, malheureusement, une erreur s'est glissée dans la consigne précédente. Le prix unitaire d'un verre de limonade est érroné. En réalité, un verre de limonade coûte 1.7e. Mettez à jour le tableau afin de prendre en compte cette information.
> 
> Qu'est-ce qui est génant dans la mise à jour de cette information?
> 
> Que peut-on faire pour palier à ce problème?

|*Personne*| Prénom | Nom | Préférence | Prix |
|:------:|:------:|:---:|:----------:|:----:|
|| Timothée | Lafontaine | cola | 1.5 |
|| Arlette | Béland | vin | 2 |
|| Anaïs | Pichette | bière | 2 |
|| Éric | Ratté | limonade | 1.7 |
|| Bruno | Aubé | vin | 2 |
|| Felicienne | Cloutier | limonade | 1.7 |
|| Simone | Bourget | limonade | 1.7 |
|| Hamilton | Camus | limonade | 1.7 |
|| Yvette | Bérard | bière | 2 |
|| Théophile | Allain | vin | 2 |
|| Hugues | Laisné | limonade | 1.7 |
|| Florence | Verreau | vin | 2 |
|| Hilaire | Ouellet | limonade | 1.7 |
|| Suzette | Lampron | cola | 1.5 |
|| Louis | Déziel | vin | 2 |

- L'information est dupliquée. De ce fait, toutes les duplication de l'information doivent être mises à jour.
- Utiliser un table auxilliaire pour stocker les boissons et leurs prix

## Exercice 4.
> Restructurez les données en deux tables: *personne* et *boisson*.
> 
> Quelle est l'implication de l'utilisation d'une table auxilliaire pour stocker les boissons préférée sur les données de la table *boisson*?
> 
> Et sur les données de la table *personne* ?

|*Personne*| Prénom | Nom | Préférence |
|:------:|:------:|:---:|:----------:|
|| Timothée | Lafontaine | cola |
|| Arlette | Béland | vin |
|| Anaïs | Pichette | bière |
|| Éric | Ratté | limonade |
|| Bruno | Aubé | vin |
|| Felicienne | Cloutier | limonade |
|| Simone | Bourget | limonade |
|| Hamilton | Camus | limonade |
|| Yvette | Bérard | bière |
|| Théophile | Allain | vin |
|| Hugues | Laisné | limonade |
|| Florence | Verreau | vin |
|| Hilaire | Ouellet | limonade |
|| Suzette | Lampron | cola |
|| Louis | Déziel | vin |

|*Boisson*| Dénomination | Prix |
|:--:|:------------:|:----:|
|| limonade | 1.7 |
|| bière | 2 |
|| cola | 1.5 |
|| vin | 2 |

- La dénomination des boisson doit être unique.
- La valeur de la préférence d'une personne doit être inclue dans les dénominations existante des personnes.
