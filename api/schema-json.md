# Schema JSON

Schema JSON pour l'envoi des trajets sur la route `POST /journeys/push`

### Propriétés

* `journey_id` : générée par l'opérateur et  doit être unique
* `operator_class` : la classe de preuve correspondant au spécifications définies dans Classes de preuve de covoiturage.

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
            lat: <Number> // float WGS84
            lon: <Number> // float WGS84
            insee: <String> // use String
            literal: <String> // human readable adresse
        }
        end: {
            datetime: <DateTime> // UTC ISO 8601 (YYYY-MM-DD hh:mm:ssZ)
            lat: <Number> // float WGS84
            lon: <Number> // float WGS84
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

