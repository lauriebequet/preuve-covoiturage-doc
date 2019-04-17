# Schema JSON

Schema JSON pour l'envoi des trajets sur la route `POST /journeys/push`

## Propriétés

**\***Données obligatoires

* `journey_id`**\*** : générée par l'opérateur et  doit être unique
* `operator_journey_id` : générée par l'opérateur pour regrouper des trajets
* `operator_class`**\*** : la classe de preuve correspondant au spécifications définies dans [Classes de preuve de covoiturage](../specifications/classes-de-preuve-de-covoiturage.md).
* `{passenger|driver}.firstname` : Prénom de l'occupant
* `{passenger|driver}.lastname` : Nom de l'occupant
* `{passenger|driver}.email` : Email de l'occupant
* `{passenger|driver}.phone`**\*** : Numéro de téléphone français au format ITU E.164 \(+33123456789\)
* `{passenger|driver}.company` : Nom de l'organisation / entreprise
* `passenger.over_18` : Le passager est majeur \(`TRUE`\) ou mineur \(`FALSE`\) ou non communiqué \(`NULL`\)
* `{passenger|driver}.cards` : Cartes de transport \(TCL, Navigo, Traboule, ...\) possédées par l'occupant. Un `Array` contenant le nom et le numéro \(obligatoire\). Si l'utilisateur ne possède pas de carte, omettre le champ totalement.
* `{passenger|driver}.{start|end}.datetime` **\*** : Date et heure du départ/arrivée au format ISO 8601 \(YYYY-MM-DDThh:mm:ssZ\).

  L'heure est exprimée en UTC \(Coordinated Universal Time\). UTC n'est pas ajusté sur l'heure d'été et hiver !

* `{passenger|driver}.{start|end}.lat` : Latitude comprise entre 90deg et -90deg décimaux en datum WSG-84
* `{passenger|driver}.{start|end}.lon` : Longitude comprise entre 180deg et -180deg décimaux en datum WSG-84
* `{passenger|driver}.{start|end}.insee` : Code INSEE commune ou arrondissement de la position.

  Pour le métropoles qui comportent un code INSEE global et des codes par arrondissement, utiliser le code arrondissement.

* `{passenger|driver}.{start|end}.literal` : Adresse litérale, par exemple: _5 rue du Paradis, 75010 Paris_, _CEA, Saclay_

> L'ordre de priorité des propriétés de position est le suivant : lon/lat, insee, literal.  
> **Au minimum une propriété doit être renseignée** \(ou deux pour le couple lon/lat\).

* `{passenger|driver}.distance` : Distance entre `start` et `end` en mètres \(10km = 10000\)
* `{passenger|driver}.duration` : Durée du trajet entre `start` et `end` en secondes \(25min = 1500\)



* `passenger.seats`**\*** : Nombre de sièges réservés par l'occupant passager. Défault : 1
* `passenger.contribution`**\*** : Coût total du service pour l’occupant passager en fonction du nombre de sièges réservés **après** une possible incitation opérateur \(subventions, promotions, etc\).
* `driver.revenue`**\*** : La somme perçue par le conducteur, comprenant les contributions des passagers, **après** une possible incitation opérateur \(subventions, promotions, etc\) et prise de commission de l’opérateur.

> Il est important d'avoir ces informations afin de s'assurer que les occupants du véhicule ne perçoivent pas un bénéfice. Ces informations sont associées avec celles paramétrées par l'AOM :

> * `driver.incentive` : Incitation donnée par l'AOM au conducteur.
> * `passenger.incentive` : Incitation donnée par l'AOM au passager.
>
> #### **Le registre procède ensuite aux calculs suivants :** 
>
> * `driver.expense` : Frais engagés par le conducteur selon le barème kilométrique \(0,558 euros / km\). Seuls les kilomètres covoiturés sont pris en compte.
> * `driver.cost` : `driver.expense - driver.revenue` : Coût pour le conducteur basé sur les frais engagés **après** avoir perçu les contributions des passagers, une possible incitation opérateur \(subventions, promotions, etc\) et prise de commission de l’opérateur.
> * `passenger.cost` : `passenger.contribution / passenger.seats` : Coût pour un passager unique.
> * **`driver.remaining_fee` : `driver.cost - driver.incentive`** : Somme restante à charge du conducteur **après** incitation de l'AOM.
> * **`passenger.remaining_fee` : `passenger.cost - passenger.incentive`** : Somme restante à charge du passager **après** incitation de l'AOM.

## Schema JSON

```javascript
{
    journey_id: <String|Number> * // operator given ID - unique !
    operator_journey_id: <String> // operator ID for the trip (1 driver, many passengers)
    operator_class: <String> * // type of proof (A, B, C)
    passenger: {
        identity: {
            firstname: <String>
            lastname: <String>
            email: <String>
            phone: <String> *
            company: <String>
            over_18: <Boolean|null> // passenger is over 18 years old : true|false|null
            cards: [
                name: <String>
                number: <String> *
            ]
        }
        start: {
            datetime: <DateTime> // UTC ISO 8601 (YYYY-MM-DD hh:mm:ssZ)
            lon: <Number> // float WGS84
            lat: <Number> // float WGS84
            insee: <String> // use String
            literal: <String> // human readable adresse
        }
        end: {
            datetime: <DateTime> // UTC ISO 8601 (YYYY-MM-DD hh:mm:ssZ)
            lon: <Number> // float WGS84
            lat: <Number> // float WGS84
            insee: <String> // use String
            literal: <String> // human readable adresse
        }
        seats: <Number> * // number of seats booked by the user (default: 1)
        contribution: <Number> * // contribution in Euro cents ex: 10€ -> 1000
        distance: <Number> // meters
        duration: <Number> // seconds
    }
    driver: {
        identity: {
            firstname: <String>
            lastname: <String>
            email: <String>
            phone: <String> *
            company: <String>
        }
        start: {
            datetime: <DateTime> * // UTC ISO 8601 (YYYY-MM-DD hh:mm:ssZ)
            lat: <Number> // float WGS84
            lon: <Number> // float WGS84
            insee: <String> // use String
            literal: <String> // human readable adresse
        }
        end: {
            datetime: <DateTime> * // UTC ISO 8601 (YYYY-MM-DD hh:mm:ssZ)
            lat: <Number> // float WGS84
            lon: <Number> // float WGS84
            insee: <String> // use String
            literal: <String> // human readable adresse
        }
        revenue: <Number> * // revenue in Euro cents ex: 10€ -> 1000 
        distance: <Number> // meters
        duration: <Number> // seconds    
    }
}
```

