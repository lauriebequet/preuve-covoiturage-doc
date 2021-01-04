# Statistiques

Chez Beta.gouv, dans une volonté de transparence, les statistiques d’usage de la majorité de nos produits sont disponibles. Les statistiques spécifiques au registre de preuve de covoiturage sont disponibles à [l'adresse suivante](https://app.covoiturage.beta.gouv.fr/stats). 

{% hint style="danger" %}
Les statistiques sont issues des données collectées à partir des informations communiquées par les opérateurs partenaires. Il ne s'agit en aucun cas d'une représentation exhaustive du covoiturage en France.
{% endhint %}

## Détails sur calcul

### Trajets réalisés 

Il s'agit du nombre de trajets en covoiturage réalisés. Un trajet correspond à un couple passager / conducteur. A chaque passager est donc affecté un trajet.

  
_Exemple : un conducteur réalise un déplacement avec deux passager différents au sein de son véhicule, le nombre de trajets réalisés et de 2._ 

### Distance parcourue

Il s'agit de la somme des distances parcourues par chacun des couples passager / conducteur. 

_Exemple : un véhicule ayant réalisé un déplacement de 10 km avec 2 passagers, la distance parcourue totale en covoiturage est de 2\*10 km = 20 km._

### Covoitureurs

Un covoitureur est un passager ou un conducteur qui a réalisé un trajet de covoiturage.

{% hint style="info" %}
A l'heure actuelle l'identité du covoitureur n'est pas pris en compte dans le calcul du nombre de covoitureurs.
{% endhint %}

### CO2 économisé

Les économies de CO2 sont calculées en partant du principe que si le passager s’est déplacé en covoiturage, alors il n’a pas utilisé son véhicule personnel. Ceci représente donc un déplacement en moins réalisé par une voiture et autant de CO2 économisé.

Les caractéristiques spécifiques des véhicules ne sont pas connus par le service. De ce fait, nous utilisons la moyenne des rejets de l’ensemble des voitures particulières immatriculées en France. Selon, l’ADEME \(Agence de l’Environnement et de la Maîtrise de l'Énergie\), les émissions moyennes de Gaz à Effet de Serre \(GES\) par véhicule et par kilomètre \(du puits à la roue\) sont de +195 g CO2 équivalent par véhicule-kilomètre \(chiffres de 2016\). 

{% hint style="info" %}
A l'heure actuelle les calculs sont effectués avec cette donnée. Pour autant, toujours selon l’ADEME, afin d’améliorer la précision de cette donnée, il convient d’appliquer un impact de

* +20% en milieu dense urbain, portant la moyenne à 234 g CO2 équivalent par véhicule-kilomètre.
* -10% sur les trajets extra-urbain, portant la moyenne à 175 g CO2 équivalent par véhicule-kilomètre.

La différenciation entre milieu dense urbain et extra-urbain n'est pas encore développée mais à termes, un algorithme calculera ensuite le produit du nombre de kilomètres parcourus par le rejet moyen de CO2 par kilomètre en fonction de la zone dans laquelle s’est réalisée le déplacement.
{% endhint %}

### Pétrole économisé

Les économies d’énergie en kilogramme équivalent pétrole \(kep\) sont calculées en partant du principe que si le passager s’est déplacé en covoiturage, alors il n’a pas utilisé son véhicule personnel. Ceci représente donc un déplacement en moins réalisé par une voiture et autant de kep économisé.

Les caractéristiques spécifiques des véhicules ne sont pas connus par le service. De ce fait, nous utilisons la moyenne kep des voitures particulières immatriculées en France. Selon, l’ADEME \(Agence de l’Environnement et de la Maîtrise de l'Énergie\), les chiffres clés 2015 - Climat, air et énergie, les kep par véhicule particulier et par kilomètre \(du puits à la roue\) sont de :

* 0, 0564 kep / km / véhicule particulier, en milieu dense urbain.
* 0,0442 kep / km / véhicule particulier sur les trajets extra-urbain.

Un algorithme calcule ensuite le produit du nombre de kilomètres parcourus par le kep par kilomètre en fonction de la zone dans laquelle s’est réalisée le déplacement.  


{% hint style="info" %}
 A l'heure actuelle, la différenciation entre milieu dense urbain et extra-urbain n'est pas encore développée ainsi à l'heure actuelle les calculs sont effectués avec une approximation de 0,05 kep / km / véhicule particulier. 

Un algorithme calcule ensuite le produit du nombre de kilomètres parcourus par le kep par kilomètre en fonction de la zone dans laquelle s’est réalisée le déplacement.
{% endhint %}

##  **Informations complémentaires**

Actuellement les dates des statistiques sont en GMT + 0 et ne prennent pas en compte les différences de fuseaux horaires. Un chantier est en cours de réalisation sur le sujet. 

Notre promesse est “retrouvez dans le registre de preuve de covoiturage, les trajets réalisés en maximum une semaine”. En effet, il peut y avoir un décalage qui peut aller jusqu'à 7 jours entre la réception d'une preuve et son affichage par le registre \(voir [explications techniques](../operateurs/envoyer-des-trajets/#quel-est-le-delai-denvoi-des-preuves-de-covoiturage)\). 

