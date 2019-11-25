---
description: Version 1.0 du schéma de preuves. Supporté jusqu'au 31 décembre 2019.
---

# Schema JSON V1 \(déprécié\)

{% hint style="danger" %}
Attention, cette version du schéma est dépréciée. Merci d'utiliser la [version 2.0](schema-json-v2.md).  
Fin du support : **31 décembre 2019**
{% endhint %}

Schéma JSON pour l'envoi des trajets sur la route `POST /journeys/push`  
Le schéma de données est présenté au format [JSON Schema Draft-07](https://json-schema.org/understanding-json-schema/index.html).

Le schéma complet est disponible à la fin de ce document. Afin de le rendre plus accessible, les données principales sont présentées en introduction.

> Voir également [Alimenter le registre via l'API](../mode-demploi/envoyer-des-trajets.md).

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
* `{passenger|driver}.travel_pass` : Carte de transport \(TCL, Navigo, Trabool, etc.\) possédée par l'occupant. Le numéro est obligatoire si l'information est disponible. Si pas de carte, passer `NULL` ou omettre le champ.

#### Liste des passes transport supportés :

Pour le moment, seul le passe `navigo` est supporté.

### Données géographiques

Les points de départ et d'arrivée du passager et du conducteur.  
`passenger.start`, `passenger.end`, `driver.start`, `driver.end`

* `datetime` \*   
  Date et heure du départ/arrivée au format ISO 8601 \(`YYYY-MM-DDThh:mm:ssZ`\).

  L'heure est exprimée en UTC \(Coordinated Universal Time\). UTC n'est pas ajusté sur l'heure d'été et hiver !

* `lat`  Latitude comprise entre 90deg et -90deg décimaux en datum WSG-84
* `lon`  Longitude comprise entre 180deg et -180deg décimaux en datum WSG-84
* `insee`   
  Code INSEE commune ou arrondissement de la position.

  Pour le métropoles qui comportent un code INSEE global et des codes par arrondissement, utiliser le code arrondissement.

* `literal`  Adresse littérale, par exemple: _5 rue du Paradis, 75010 Paris_, _CEA, Saclay_
* `country`  _Nom complet du pays \(New-Zealand, France, etc.\)_

> L'ordre de priorité des propriétés de position est le suivant : lon/lat, insee, literal.  
> **Au minimum une propriété doit être renseignée** \(ou deux pour le couple lon/lat\).

### Données du trajet

* `distance`  Distance entre `start` et `end` en **mètres** \(10km = 10000\)
* `duration`  Durée du trajet entre `start` et `end` en **secondes** \(25min = 1500\)

### Données financières 

{% hint style="info" %}
Le principe est de coller au plus près avec la réalité comptable \(transaction usager\) et d'avoir suffisamment d'informations pour recalculer le coût initial du trajet. Ceci afin de s'assurer du respect de la définition du covoiturage et de la bonne application des politiques incitatives gérées par le registre.
{% endhint %}

{% hint style="warning" %}
Les montants financiers sont exprimés en centimes d'euros
{% endhint %}

* `passenger.contribution`**\***  Coût réel total du service pour l’occupant passager en fonction du nombre de sièges réservés **APRÈS** que toutes les possibles incitations aient été versées \(subventions employeurs, promotions opérateurs, incitations AOM, etc\).
* `driver.revenue`**\***  La somme réellement perçue par le conducteur **APRÈS** que toutes les incitations \(subventions employeurs, promotions opérateurs, incitations AOM, etc.\), contributions des passagers aient été versées et que la commission de l’opérateur soit prise.
* `passenger.seats`**\*** : Nombre de sièges réservés par l'occupant passager. Défaut : 1
* `passenger.incentive`  Montant de l'incitation versée par l'opérateur au passager. _Ce montant est converti vers le nouveau schéma en utilisant le SIRET de l'opérateur._ [_Voir la spécification pour les détails_](schema-json-v2.md#donnees-financieres)_._

## Schema JSON complet

```javascript
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "Registre de preuve de covoiturage - Journey Schema V1",
  "$id": "rpc.journey.v1",
  "definitions": {
    "travelpass": {
      "type": "object",
      "minProperties": 2,
      "additionalProperties": false,
      "properties": {
        "name": {
          "enum": ["navigo"]
        },
        "user_id": {
          "macro": "varchar"
        }
      }
    },
    "identity": {
      "type": "object",
      "required": [
        "phone"
      ],
      "additionalProperties": false,
      "properties": {
        "firstname": {
          "macro": "varchar"
        },
        "lastname": {
          "macro": "varchar"
        },
        "email": {
          "macro": "email"
        },
        "phone": {
          "macro": "phone"
        },
        "company": {
          "macro": "varchar"
        },
        "over_18": {
          "enum": [true, false, null],
          "default": null
        }
      }
    },
    "position": {
      "type": "object",
      "required": [
        "datetime"
      ],
      "additionalProperties": false,
      "minProperties": 2,
      "dependencies": {
        "lat": ["lon"],
        "lon": ["lat"],
        "country": ["literal"]
      },
      "properties": {
        "datetime": {
          "macro": "timestamp"
        },
        "lat": {
          "macro": "lat"
        },
        "lon": {
          "macro": "lon"
        },
        "insee": {
          "macro": "insee"
        },
        "town": {
          "macro": "varchar"
        },
        "country": {
          "macro": "varchar"
        },
        "literal": {
          "macro": "longchar"
        }
      }
    },
    "payment": {
      "type": "object",
      "required": [
        "pass",
        "amount"
      ],
      "additionalProperties": false,
      "properties": {
        "pass": {
          "macro": "siret"
        },
        "amount": {
          "type": "integer",
          "minimum": 0,
          "maximum": 100000
        }
      }
    },
    "passenger": {
      "type": "object",
      "required": [
        "identity",
        "start",
        "end"
      ],
      "additionalProperties": false,
      "properties": {
        "identity": {
          "$ref": "#/definitions/identity"
        },
        "start": {
          "$ref": "#/definitions/position"
        },
        "end": {
          "$ref": "#/definitions/position"
        },
        "seats": {
          "type": "integer",
          "default": 1,
          "minimum": 1,
          "maximum": 8
        },
        "cost": {
          "type": "integer",
          "minimum": 0,
          "maximum": 1000000
        },
        "contribution": {
          "type": "integer",
          "minimum": 0,
          "maximum": 1000000,
          "$comment": "Montant en centimes d'Euros après que toutes les incitations aient été attribuées"
        },
        "incentive": {
          "type": "integer",
          "minimum": 0,
          "maximum": 1000000,
          "$comment": "Incitation en centimes d'Euros"
        },
        "payments": {
          "type": "array",
          "minItems": 0,
          "items": {
            "$ref": "#/definitions/payment"
          }
        },
        "distance": {
          "type": "integer",
          "minimum": 0,
          "maximum": 1000000
        },
        "duration": {
          "type": "integer",
          "minimum": 0,
          "maximum": 86400
        },
        "travel_pass": {
          "oneOf": [{"$ref": "#/definitions/travelpass"}, {"type": "null"}]
        }
      }
    },
    "driver": {
      "type": "object",
      "required": [
        "identity",
        "start",
        "end",
        "revenue"
      ],
      "additionalProperties": false,
      "properties": {
        "identity": {
          "$ref": "#/definitions/identity"
        },
        "start": {
          "$ref": "#/definitions/position"
        },
        "end": {
          "$ref": "#/definitions/position"
        },
        "cost": {
          "type": "integer",
          "minimum": 0,
          "maximum": 1000000
        },
        "revenue": {
          "type": "integer",
          "minimum": 0,
          "maximum": 1000000,
          "$comment": "Montant perçu en centimes d'Euros après que toutes les incitations et contributions des passagers aient été attribuées"
        },
        "payments": {
          "type": "array",
          "minItems": 0,
          "items": {
            "$ref": "#/definitions/payment"
          }
        },
        "distance": {
          "type": "integer",
          "minimum": 0,
          "maximum": 1000000
        },
        "duration": {
          "type": "integer",
          "minimum": 0,
          "maximum": 86400
        }
      }
    }
  },
  "type": "object",
  "required": [
    "journey_id",
    "operator_class"
  ],
  "anyOf": [{"required": ["passenger"]}, {"required": ["driver"]}],
  "additionalProperties": false,
  "properties": {
    "journey_id": {
      "macro": "varchar"
    },
    "operator_journey_id": {
      "macro": "varchar"
    },
    "operator_class": {
      "enum": ["A", "B", "C"]
    },
    "passenger": {
      "$ref": "#/definitions/passenger"
    },
    "driver": {
      "$ref": "#/definitions/driver"
    }
  }
}
```

