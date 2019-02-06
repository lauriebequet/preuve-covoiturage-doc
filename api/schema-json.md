# Schema JSON

Schema JSON pour l'envoi des trajets sur la route `POST /journeys/push`

### Propriétés

* `journey_id` : générée par l'opérateur et  doit être unique
* `operator_class` : la classe de preuve correspondant au spécifications définies dans Classes de preuve de covoiturage.
* `{passenger|driver}.firstname` : Prénom de l'occupant
* `{passenger|driver}.lastname` : Nom de l'occupant
* `{passenger|driver}.email` : Email de l'occupant
* `{passenger|driver}.phone` : Numéro de téléphone français au format ITU E.164 (+33123456789)
* `{passenger|driver}.company` : Nom de l'organisation / entreprise
* `passenger.over_18` : Le passager est majeur (`TRUE`) ou mineur (`FALSE`)
* `{passenger|driver}.{start|end}.datetime` : Date et heure du départ/arrivée au format ISO 8601 (YYYY-MM-DD hh:mm:ssZ).
  L'heure est exprimée en UTC (Coordinated Universal Time). UTC n'est pas ajusté sur l'heure d'été et hiver !
* `{passenger|driver}.{start|end}.lon` : Longitude comprise entre 180deg et -180deg décimaux en datum WSG-84
* `{passenger|driver}.{start|end}.lat` : Longitude comprise entre 90deg et -90deg décimaux en datum WSG-84
* `{passenger|driver}.{start|end}.insee` : Code INSEE commune ou arrondissement de la position.
  Pour le métropoles qui comportent un code INSEE global et des codes par arrondissement, utiliser le code arrondissement.
* `{passenger|driver}.{start|end}.literal` : Adresse litérale, par exemple: _5 rue du Paradis, 75010 Paris_, _CEA, Saclay_

> L'ordre de priorité des propriétés de position est le suivant : lon/lat, insee, literal.  
  Au minimum une propriété doit être renseignée (ou deux pour le couple lon/lat).

* `passenger.seats` : Nombre de sièges réservés par l'occupant. Défault : 1
* `passenger.cost` : Coût du service avant subventions, promotions, etc.
* `passenger.operator_subsidy` : Subvention ou promotion donnée par l'opérateur de covoiturage

> Le montant payé par l'occupant est égal à `cost - operator_subsidy`. Il est important d'avoir
  l'information de coût du trajet afin de s'assurer que la somme de toutes les subventions
  apportées par les différents organismes (opérateurs, AOM, etc.) n'est pas supérieure au coût.

> Le coût pour le conducteur sera calculé sur la base du barême kilométrique pondéré (0,552€ / km).  
  Seuls les kilomètres covoiturés seront pris en compte.

* `{passenger|driver}.distance` : Distance entre `start` et `end` en mètres (10km -> 10000)
* `{passenger|driver}.duration` : Durée du trajet entre `start` et `end` en secondes (25min -> 1500)

### Schema JSON

```javascript
{
    journey_id: <String|Number> * // operator given ID
    operator_class: <String> * // type of proof (A, B, C)
    passenger: {
        identity: {
            firstname: <String>
            lastname: <String>
            email: <String>
            phone: <String> *
            company: <String>
            over_18: <Boolean|null> // passenger is over 18 years old : true|false|null
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
        seats: <Number> // number of seats booked by the user (default: 1)
        cost: <Number> // cost in Euro cents ex: 10€ -> 1000
        operator_subsidy: <Number> // subsidy in Euro cents ex: 10€ -> 1000
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
        distance: <Number> // meters
        duration: <Number> // seconds
    }
}
```

