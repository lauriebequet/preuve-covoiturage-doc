# Open Data - Ouverture des données

## Pourquoi ?

L’open data consiste à ouvrir, c’est-à-dire diffuser, des informations permettant notamment de garantir la transparence administrative. Les administrations sont dans l’obligation de diffuser les informations publiques qu’elles produisent ou reçoivent. L’ouverture de ces données est soumise à un cadre précis, la diffusion de ces données ne devant porter atteinte **ni à la protection de la vie privée, ni au secret des affaires**. Ainsi, nous veillons à traiter l’ensemble des informations avant leur publication.

## Où ?

data.gouv.fr est la plateforme de diffusion de données publiques \(« open data »\) de l'État français. data.gouv.fr est développé par [Etalab](https://www.etalab.gouv.fr/qui-sommes-nous).

Les jeux de données du registre de preuve de covoiturage sont déposés sur data.gouv.fr via un compte dédié \([voir profil](https://www.data.gouv.fr/fr/users/registre-de-preuve-de-covoiturage/)\).

## Quand ?

Les données relatives aux trajets contenus dans le registre de preuve de covoiturage sont ouvertes après avoir fait l’objet d’un traitement permettant une publication conforme \(anonymisation, agrégation, etc.\). Aujourd'hui ce traitement n'est pas automatisé et de ce fait la fréquence d'ouverture n'est pas définitive. Un jeu de donnée correspond aux trajets sur un mois.

## Comment ?

Dans le cadre de l'ouverture des données, les principaux traitements effectués sont les suivants :

* Anonymisation des données via la suppression des identifiants conducteurs et passagers.
* Application de tranches horaires : les heures de départs et arrivées sont arrondis au quart d'heure près.
* Carroyage des données géographiques :
  * Lorsque la densité du point de départ ou arrivée est faible : la latitude et longitude sont tronqués à 2 décimales _\(précision de ~700m\)_.
  * Lorsque la densité du point de départ ou arrivée est forte : la latitude et longitude sont tronqués à 3 décimales _\(précision de ~70m\)_.
* Suppression des trajets afférents à une maille géographique "solitaire" : 
  * Si le nombre d'occurences du code INSEE de départ est &lt; 6 sur le jeu de données, le trajet est supprimé.
  * Si le nombre d'occurences du code INSEE d'arrivée est &lt; 6 sur le jeu de données, le trajet est supprimé.

Ces mesures permettent ainsi de limiter la réidentification. Dans la description du jeu de données, le nombre de trajets supprimés est indiqué.

## Format ?

Chaque ligne correspond à un trajet de covoiturage, c'est à dire un couple passager / conducteur. A chaque passager est donc affecté un trajet.

Exemple : un conducteur réalise un déplacement avec deux passagers différents au sein de son véhicule, le nombre de trajets réalisés et de 2. Ceci se traduit par deux lignes.

* `trip_id`

  Identifiant permettrant de recouper plusieurs couples passager/conducteur dans un même véhicule. 

  _Exemple : c4124bb1-d8a4-487c-b4d9-367b931ee8ce_

* `journey_start_datetime`

  _Exemple : 2019-10-31T23:00:00.000Z_

  Date et heure du départ au format ISO 8601 \(YYYY-MM-DDThh:mm:ssZ\).

  L'heure est exprimée en UTC \(Coordinated Universal Time\). UTC n'est pas ajusté sur l'heure d'été et hiver !

* `journey_start_lat`    

  _Exemple : 48.725_

  Latitude du point de départ \(prise en charge passager\) comprise entre 90deg et -90deg décimaux en datum WSG-84

* `journey_start_lon`    

  Exemple : 2.261

  Longitude du point de départ \(prise en charge passager\) comprise entre 180deg et -180deg décimaux en datum WSG-84

* `journey_start_insee`    

  _Exemple : 91377_

  Code INSEE commune ou arrondissement du point de départ \(prise en charge passager\).

* `journey_start_postcode`

  _Exemple : 91300_

  Code postal du point de départ \(prise en charge passager\)

* `journey_start_town`    

  _Exemple : Massy_

  Commune du point de départ \(prise en charge passager\)

* `journey_start_country`    

  _Exemple : France_

  Pays du point de départ \(prise en charge passager\)

* `journey_end_datetime`    

  _Exemple : 2019-10-31T23:15:00.000Z_

  Date et heure de l'arrivée au format ISO 8601 \(YYYY-MM-DDThh:mm:ssZ\).

  L'heure est exprimée en UTC \(Coordinated Universal Time\). UTC n'est pas ajusté sur l'heure d'été et hiver !

* `journey_end_lat`    

  _Exemple : 48.695_

  Latitude du point d'arrivée \(dépose passager\) comprise entre 90deg et -90deg décimaux en datum WSG-84

* `journey_end_lon`    

  _Exemple : 2.162_

  Longitude du point d'arrivée \(dépose passager\) comprise entre 180deg et -180deg décimaux en datum WSG-84

* `journey_end_insee`    

  _Exemple : 91122_

  Code INSEE commune ou arrondissement du point d'arrivée \(dépose passager\).

* `journey_end_postcode`    

  _Exemple : 91440_

  Code postal du point d'arrivée \(dépose passager\)

* `journey_end_town`    

  _Exemple : Bures-sur-Yvette_

  Commune du point d'arrivée \(dépose passager\)

* `journey_end_country`

  _Exemple : France_

  Pays du point d'arrivée \(dépose passager\)

### Attention

Ces données sont collectées à partir des informations communiquées par les [opérateurs partenaires](http://covoiturage.beta.gouv.fr/#operateurs). En outre il ne saurait s'agir :

* d'une représentation exhaustive du covoiturage en France ;
* d'un outil permettant le calcul de part de marché d'un acteur du covoiturage.

## Contacts

Pour toute demande d’information, veuillez contacter l'équipe du registre de preuve de covoiturage à l’adresse suivante : technique@covoiturage.beta.gouv.fr Nous vous remercions de bien vouloir renseigner l'objet de votre mail comme suit : OpenDataRPC-votre nom.

