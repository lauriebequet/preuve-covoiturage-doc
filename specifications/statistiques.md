# Statistiques

Chez Beta.gouv, dans une volonté de transparence, les statistiques d’usage de la majorité de nos produits sont disponibles. Les statistiques spécifiques au registre de preuve de covoiturage sont disponibles à [l'adresse suivante](https://app.covoiturage.beta.gouv.fr/stats). 

{% hint style="danger" %}
Les statistiques sont issues des données collectées à partir des informations communiquées par les opérateurs partenaires. Il ne s'agit en aucun cas d'une représentation exhaustive du covoiturage en France.
{% endhint %}

## Détails sur calcul

### Trajets réalisés 

{% hint style="info" %}
_Unité : trajets réalisés_
{% endhint %}

Il s'agit du nombre de trajets en covoiturage réalisés. Un trajet correspond à un couple passager / conducteur. A chaque passager est donc affecté un trajet.

_Exemple : un conducteur réalise un déplacement avec deux passager différents au sein de son véhicule, le nombre de trajets réalisés et de 2._

Cet indicateur tient également compte du nombre de sièges réservés par un passager.

_Exemple : un passager fait une réservation pour son propre compte et le compte de son ami, le nombre de trajets réalisés et de 2._

### Distance parcourue

{% hint style="info" %}
_Unité : km parcourus_
{% endhint %}

Il s'agit de la somme des distances parcourues par chacun des couples passager / conducteur.

_Exemple : un véhicule ayant réalisé un déplacement de 10 km avec 2 passagers, la distance parcourue totale en covoiturage est de 210 km = 20 km._

Cet indicateur tient également compte du nombre de sièges réservés par un passager.

_Exemple : un passager fait une réservation pour son propre compte et le compte de son ami pour un trajet de 10 km, la distance parcourue totale en covoiturage est de 2x10 km = 20 km._

### Covoitureurs

{% hint style="info" %}
_Unité : covoitureur⸱euses_
{% endhint %}

Un⸱e covoitureur⸱euse est un⸱ passager⸱e ou un⸱ conducteur⸱euse qui a réalisé un trajet de covoiturage. Cette statistique se base sur l'identifiant unique communiqué par l'opérateur utilisé et a pour objectif d'estimer le nombre de personne touchée par le covoiturage. Il vaut pour 1 à compter de son premier voyage avec un opérateur donné. Exemples :

* un⸱e conducteur⸱rice réalise son premier déplacement sur une application avec un nouveau passager, la somme des covoitureur⸱euses est itérée de 2.
* un⸱e conducteur⸱rice réalise son premier déplacement sur une application avec un⸱e passager⸱e habitué⸱e, la somme des covoitureur⸱euses est itérée de 1.
* un⸱e conducteur⸱rice habitué⸱e à une platefome réalise pour la première fois un déplacement sur une nouvelle plateforme avec un passager habitué, la somme des covoitureurs est itérée de 1 \(_pas d'identifiant interplateforme_\)

### CO2 économisé

{% hint style="info" %}
_Unité : t eq CO₂ économisées_
{% endhint %}

Les économies de CO2 sont calculées en partant du principe que si le passager s’est déplacé en covoiturage, alors il n’a pas utilisé son véhicule personnel. Ceci représente donc un déplacement en moins réalisé par une voiture et autant de CO2 économisé. Les caractéristiques spécifiques des véhicules ne sont pas connues par le service. De ce fait, nous utilisons la moyenne des rejets de l’ensemble des voitures particulières immatriculées en France. Selon, l’ADEME \(Agence de l’Environnement et de la Maîtrise de l'Énergie\), les émissions moyennes de Gaz à Effet de Serre \(GES\) par véhicule et par kilomètre \(du puits à la roue\) sont de +195 g CO2 équivalent par véhicule-kilomètre \(chiffres de 2016\).

Un algorithme calcule ensuite le produit du nombre de kilomètres parcourus par le rejet moyen de CO2 par kilomètre. Cet indicateur tient également compte du nombre de sièges réservés par un passager.

### Pétrole économisé

{% hint style="info" %}
_Unité : l d'essence économisés_
{% endhint %}

Les économies d’énergie en kilogramme équivalent pétrole \(kep\) sont calculées en partant du principe que si le passager s’est déplacé en covoiturage, alors il n’a pas utilisé son véhicule personnel. Ceci représente donc un déplacement en moins réalisé par une voiture et autant de kep économisé. Les caractéristiques spécifiques des véhicules ne sont pas connues par le service. De ce fait, nous utilisons la moyenne kep des voitures particulières immatriculées en France. Selon, l’ADEME \(Agence de l’Environnement et de la Maîtrise de l'Énergie\), les chiffres clés 2015 - Climat, air et énergie, les kep par véhicule particulier et par kilomètre \(du puits à la roue\) sont de 0,05 kep / km / véhicule particulier en moyenne.

Un algorithme calcule ensuite le produit du nombre de kilomètres parcourus par le kep par kilomètre. Cet indicateur tient également compte du nombre de sièges réservés par un passager. 

### Opérateurs

{% hint style="info" %}
_Unité : opérateur\(s\) actif\(s\)_
{% endhint %}

Un opérateur désigne une personne morale opérant un service de covoiturage pour mettre en relation les covoitureurs. Le nombre d'opérateur correspond à la somme des services de covoiturage différents actifs. Un service est considéré comme actif à partir du moment où un trajet a été remonté. A titre d'exemple sur le période du 1 au 15 juin 2020, si l'opérateur A fait remonter 5 trajets, que l'opérateur B fait remonter 1 trajet et que l'opérateur C a fait remonter 0 trajet, alors l'indicateur sera de "2 opérateur\(s\)".

### **Equipage moyen**

{% hint style="info" %}
_Unité : personnes par véhicule_
{% endhint %}

Il s'agit d'un indicateur représentant l'équipage moyen d'un covoiturage. Cet indicateur tient également compte du nombre de sièges réservés par un passager.

_Exemple : en considérant sur une période donnée 4 trajets \(couple passager-conducteur\). 1. Un trajet conducteur A / passager B \(nombre de siège réservé = 1\) 2. Un trajet conducteur A / passager C \(nombre de siège réservé = 2\) 3. Un trajet conducteur D / passager E \(nombre de siège réservé = 1\) 4. Un trajet conducteur D / passager F \(nombre de siège réservé = 1\) L'indicateur est \(\(1+2\)+\(1+1\)\)/2 = 2,5 passagers par véhicule d'où 3,5 personnes par véhicule_

### **Incitations financières**

{% hint style="info" %}
_Unité : € distribués_
{% endhint %}

Il s'agit de la somme des contreparties financières distribuées par une AOM à des covoitureurs répondants aux critères de politiques d'incitation. Cet indicateur est propre à une AOM et ne prend pas en compte les incitations distribuées par d'autres organismes incitateurs.

### **Incitations non financières**

{% hint style="info" %}
_Unité : points distribués_
{% endhint %}

Il s'agit de la somme des points équivalents à des contreparties non financières distribués par une AOM à des covoitureurs répondants aux critères de politiques d'incitation. Cet indicateur est propre à une AOM et ne prend pas en compte les incitations distribuées par d'autres organismes incitateurs.

## **Informations complémentaires**

Actuellement les dates des statistiques sont en GMT + 0 et ne prennent pas en compte les différences de fuseaux horaires. Un chantier est en cours de réalisation sur le sujet. 

Notre promesse est “retrouvez dans le registre de preuve de covoiturage, les trajets réalisés en maximum une semaine”. En effet, il peut y avoir un décalage qui peut aller jusqu'à 7 jours entre la réception d'une preuve et son affichage par le registre \(voir [explications techniques](../operateurs/envoyer-des-trajets/#quel-est-le-delai-denvoi-des-preuves-de-covoiturage)\). 

