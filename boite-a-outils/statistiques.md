# Statistiques

Chez Beta.gouv, dans une volonté de transparence, les statistiques d’usage de la majorité de nos produits sont disponibles. Les statistiques spécifiques au registre de preuve de covoiturage sont disponibles à [l'adresse suivante](https://app-staging.covoiturage.beta.gouv.fr/statistics). 

## Détails sur calcul

### Distance parcourue

Il s'agit de la somme des distances parcourues en covoiturage. Sont prises en compte les distances uniquement covoiturées à partir de la prise en charge d'un passager et jusqu'à la dépose du dernier passager. 

### CO2 economisé

Les économies de CO2 sont calculées en partant du principe que si le passager s’est déplacé en covoiturage, alors il n’a pas utilisé son véhicule personnel. Ceci représente donc un déplacement en moins réalisé par une voiture et autant de CO2 économisé.

Les caractéristiques spécifiques des véhicules ne sont pas connus par le service. De ce fait, nous utilisons la moyenne des rejets de l’ensemble des voitures particulières immatriculées en France. Selon, l’ADEME \(Agence de l’Environnement et de la Maîtrise de l'Énergie\), les émissions moyennes de Gaz à Effet de Serre \(GES\) par véhicule et par kilomètre \(du puits à la roue\) sont de +195 g CO2 équivalent par véhicule-kilomètre \(chiffres de 2016\). 

NB : A l'heure actuelle les calculs sont effectués avec cette donnée. Pour autant, toujours selon l’ADEME, afin d’améliorer la précision de cette donnée, il convient d’appliquer un impact de

* +20% en milieu dense urbain, portant la moyenne à 234 g CO2 équivalent par véhicule-kilomètre.
* -10% sur les trajets extra-urbain, portant la moyenne à 175 g CO2 équivalent par véhicule-kilomètre.

La différenciation entre milieu dense urbain et extra-urbain n'est pas encore développée mais à termes, un algorithme calculera ensuite le produit du nombre de kilomètres parcourus par le rejet moyen de CO2 par kilomètre en fonction de la zone dans laquelle s’est réalisée le déplacement.

### Pétrole économisé

Les économies d’énergie en kilogramme équivalent pétrole \(kep\) sont calculées en partant du principe que si le passager s’est déplacé en covoiturage, alors il n’a pas utilisé son véhicule personnel. Ceci représente donc un déplacement en moins réalisé par une voiture et autant de kep économisé.

Les caractéristiques spécifiques des véhicules ne sont pas connus par le service. De ce fait, nous utilisons la moyenne kep des voitures particulières immatriculées en France. Selon, l’ADEME \(Agence de l’Environnement et de la Maîtrise de l'Énergie\), les chiffres clés 2015 - Climat, air et énergie, les kep par véhicule particulier et par kilomètre \(du puits à la roue\) sont de :

* 0, 0564 kep / km / véhicule particulier, en milieu dense urbain.
* 0,0442 kep / km / véhicule particulier sur les trajets extra-urbain.

Un algorithme calcule ensuite le produit du nombre de kilomètres parcourus par le kep par kilomètre en fonction de la zone dans laquelle s’est réalisée le déplacement.  


NB : La différenciation entre milieu dense urbain et extra-urbain n'est pas encore développée ainsi à l'heure actuelle les calculs sont effectués avec une approximation de 0,05 kep / km / véhicule particulier. 

Un algorithme calcule ensuite le produit du nombre de kilomètres parcourus par le kep par kilomètre en fonction de la zone dans laquelle s’est réalisée le déplacement.  


