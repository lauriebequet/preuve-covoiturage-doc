# Schema JSON

Schema JSON pour l'envoi des trajets sur la route `POST /journeys/push`

## Propriétés

**\*** Données obligatoires

* `journey_id`**\*** : générée par l'opérateur et doit être unique
* `operator_journey_id` : générée par l'opérateur pour regrouper des trajets
* `operator_class`**\*** : la classe de preuve correspondant au spécifications définies dans [Classes de preuve de covoiturage](../specifications/classes-de-preuve-de-covoiturage.md).

### Données sur l'identité de l'occupant

* `{passenger|driver}.firstname` : Prénom de l'occupant
* `{passenger|driver}.lastname` : Nom de l'occupant
* `{passenger|driver}.email` : Email de l'occupant
* `{passenger|driver}.phone`**\*** : Numéro de téléphone au format ITU E.164 \(+33123456789\)
* `{passenger|driver}.company` : Nom de l'organisation / employeur
* `passenger.over_18` : Le passager est majeur \(`TRUE`\) ou mineur \(`FALSE`\) ou non communiqué \(`NULL`\)
* `{passenger|driver}.travel_pass` : Carte de transport \(TCL, Navigo, Trabool, etc.\) possédée par l'occupant. Le numéro est obligatoire si l'information est disponible.

#### Liste des Pass transport supportés :

La liste complète est disponible dans le fichier de configuration de l'API. _\(à venir\)_  
Vous pouvez soumettre des modifications en créant une _Pull Request_ directement sur _Repository_ du projet \(un compte Github est requis\).

### Données sur le trajet 

* `{passenger|driver}.{start|end}.datetime` **\*** : Date et heure du départ/arrivée au format ISO 8601 \(YYYY-MM-DDThh:mm:ssZ\).

  L'heure est exprimée en UTC \(Coordinated Universal Time\). UTC n'est pas ajusté sur l'heure d'été et hiver !

* `{passenger|driver}.{start|end}.lat` : Latitude comprise entre 90deg et -90deg décimaux en datum WSG-84
* `{passenger|driver}.{start|end}.lon` : Longitude comprise entre 180deg et -180deg décimaux en datum WSG-84
* `{passenger|driver}.{start|end}.insee` : Code INSEE commune ou arrondissement de la position.

  Pour le métropoles qui comportent un code INSEE global et des codes par arrondissement, utiliser le code arrondissement.

* `{passenger|driver}.{start|end}.literal` : Adresse littérale, par exemple: _5 rue du Paradis, 75010 Paris_, _CEA, Saclay_
* _`{passenger|driver}.{start|end}.country` : Nom complet du pays \(New-Zealand, France, etc.\)_

> L'ordre de priorité des propriétés de position est le suivant : lon/lat, insee, literal.  
> **Au minimum une propriété doit être renseignée** \(ou deux pour le couple lon/lat\).

* `{passenger|driver}.distance` : Distance entre `start` et `end` en mètres \(10km = 10000\)
* `{passenger|driver}.duration` : Durée du trajet entre `start` et `end` en secondes \(25min = 1500\)

### Données financières 

{% hint style="info" %}
Le principe est de coller au plus près avec la réalité comptable \(transaction usager\) et d'avoir suffisamment d'informations pour recalculer le coût initial du trajet. Ceci afin de s'assurer du respect de la définition du covoiturage et de la bonne application des politiques incitatives gérées par le registre.
{% endhint %}

* `passenger.contribution`**\*** : Coût réel total du service pour l’occupant passager en fonction du nombre de sièges réservés **APRÈS** que toutes les possibles incitations aient été versées \(subventions employeurs, promotions opérateurs, incitations AOM, etc\).
* `driver.revenue`**\*** : La somme réellement perçue par le conducteur **APRÈS** que toutes les incitations \(subventions employeurs, promotions opérateurs, incitations AOM, etc.\), contributions des passagers aient été versées et que la commission de l’opérateur soit prise.
* `passenger.seats`**\*** : Nombre de sièges réservés par l'occupant passager. Défault : 1

**Schéma des incitations** 

* `incentives` \* : Tableau reprenant la liste complète des incitations appliquées \(ordre d'application, montant, identifiant de l'incitateur\). Si aucune incitation, envoyer un tableau vide : `[]`

```text
{
    index: <Number> *         // ordre d'application [0,1,2]
    amount: <Number> *        // montant de l'incitation en centimes d'euros
    siret: <String> *         // Numéro SIRET de l'incitateur
}
```

> Le SIRET est un identifiant unique par structure juridique. Toutes les entités incitatrices en possèdent un.

Par défaut, l'ordre d'application des politiques incitatives est le suivant : 

1. AOM 
2. Sponsors \(incitations employeur, CE, etc.\) 
3. Opérateur \(opération promotionnelle, offres, etc.\)

**Schéma du mode de paiement sous forme de Titre-Mobilité**

{% hint style="info" %}
La prise en charge des frais de transports personnel \(carburant et forfait mobilité\) pourra prendre la forme d’une solution de paiement spécifique, dématérialisée et prépayée, intitulée « titre-mobilité ». Ainsi, il apparaît comme pertinent de détailler la solution de paiement utilisée dans le cadre d'un trajet covoituré, s'il s'agit de Titre-Mobilité. 
{% endhint %}

* `payments` : Zéro, une ou plusieurs méthodes de paiement utilisées

```text
{
    pass_type: <String> *     // identifiant du titre (voir ci-dessous)
    amount: <Number> *       // montant en centimes d'euros
}
```

#### Liste des Titres-Mobilité supportés :

La liste complète est disponible dans le fichier de configuration de l'API. _\(à venir\)_  
Vous pouvez soumettre des modifications en créant une _Pull Request_ directement sur _Repository_ du projet \(un compte Github est requis\).

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
            travel_pass:
                name: <String> *
                user_id: <String> *
        }
        start: {
            datetime: <DateTime> // UTC ISO 8601 (YYYY-MM-DD hh:mm:ssZ)
            lon: <Number> // float WGS84
            lat: <Number> // float WGS84
            insee: <String> // use String
            literal: <String> // human readable adresse
            country: <String> // required if literal is used
        }
        end: {
            datetime: <DateTime> // UTC ISO 8601 (YYYY-MM-DD hh:mm:ssZ)
            lon: <Number> // float WGS84
            lat: <Number> // float WGS84
            insee: <String> // use String
            literal: <String> // human readable adresse
            country: <String> // required if literal is used
        }
        distance: <Number> // meters
        duration: <Number> // seconds
        seats: <Number> * // number of seats booked by the user (default: 1)
        expense: <Number> // Optional: sent or calculated by the register in Euro cents ex: 10€ -> 1000 
        contribution: <Number> * // contribution in Euro cents ex: 10€ -> 1000
        incentives: [{
            index: <Number>
            amount: <Number>
            siren: <String>
        }]
        payments: [{
            pass_type: <String>
            amount: <Number>
        }]
    }
    driver: {
        identity: {
            firstname: <String>
            lastname: <String>
            email: <String>
            phone: <String> *
            company: <String>
            travel_pass:
                name: <String> *
                user_id: <String> *
        }
        start: {
            datetime: <DateTime> * // UTC ISO 8601 (YYYY-MM-DD hh:mm:ssZ)
            lat: <Number> // float WGS84
            lon: <Number> // float WGS84
            insee: <String> // use String
            literal: <String> // human readable adresse
            country: <String> // required if literal is used
        }
        end: {
            datetime: <DateTime> * // UTC ISO 8601 (YYYY-MM-DD hh:mm:ssZ)
            lat: <Number> // float WGS84
            lon: <Number> // float WGS84
            insee: <String> // use String
            literal: <String> // human readable adresse
            country: <String> // required if literal is used
        }
        distance: <Number> // meters
        duration: <Number> // seconds
        expense: <Number> // Optional: send or calculated by the register in Euro cents ex: 10€ -> 1000 
        revenue: <Number> * // revenue in Euro cents ex: 10€ -> 1000
        incentives: [{
            index: <Number>
            amount: <Number>
            siren: <String>
        }]
    }
}
```

