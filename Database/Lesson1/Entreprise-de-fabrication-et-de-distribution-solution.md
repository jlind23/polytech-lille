# Entreprise de fabrication et de distribution

Une entreprise de fabrication et de distribution de matériels possède une usine et plusieurs lieux de
stockage/expédition.
Un produit est caractérisé par un numéro (numP), un libellé (libP) et un prix unitaire (pu).
Chaque produit peut être stocké dans un ou plusieurs dépôts, un dépôt étant caractérisé par un numéro (numD).
Dans chaque dépôt, on connaît la quantité en stock de chaque produit (qtS) et la quantité disponible (qtD) (la différence représente la quantité réservée pour des commandes déjà validées mais non livrées).
Un client est déterminé par son numéro (numCl), son nom (nom), son prénom (prenom), son adresse (ad), le total de son chiffre d’affaire (ca) et le taux de réduction (red).
Chaque client est livré à partir d’un dépôt.
A un client peuvent être associées une ou plusieurs commandes, chacune étant caractérisée par un numéro (numCo) une date (dateC), un code produit et la quantité commandée (qtC).

Donnez les relations ainsi que les contraintes de clé primaire et de clé étrangère nécessaire pour implémenter cette base de données.

# Solution

produit(<ins>numP</ins>,libP,pu)

depot(<ins>numD</ins>)

stock(<ins>\#numP,\#numD</ins>,qtS,qtD)

client(<ins>numCl</ins>, nom, prenom, ad, ca, red, \#numD)

commande(<ins>numCo</ins>, dateC, \#numCl, \#numP, qtC)
