# Schema CSV

Il est possible durant la phase d’expérimentation d’envoyer les données à [contact@covoiturage.beta.gouv.fr](mailto:contact@covoiturage.beta.gouv.fr) au format CSV.

## Contraintes

* 1 entrée par ligne
* encodage : `UTF-8`
* tous les champs de type `String` sont entre `"`
* les `Number` ne sont pas entre guillemets: `"chaine",1.123,333`
* le séparateur décimal est un point `.` \(et non une virgule `,`\)
* les `Boolean` sont littéraux: `"TRUE":"FALSE"`
* les `Date` sont au format _UTC ISO 8601_
* séparateur: `,`
* les valeurs nulles sont vides : `"chaine 1",,"valeur à gauche est nulle"`
* nombre maximum de lignes par fichier: 100000
* **pas** de headers dans le fichier \(la première ligne contient des données\)

```text
journey_id                         // String
operator_class                     // String
passenger.identity.firstname       // String
passenger.identity.lastname        // String
passenger.identity.email           // String
passenger.identity.phone           // String
passenger.identity.company         // String
passenger.identity.over_18         // Boolean
passenger.start.datetime           // Date as String
passenger.start.lat                // Number
passenger.start.lon                // Number
passenger.start.insee              // String
passenger.start.literal            // String
passenger.end.datetime             // Date as String
passenger.end.lat                  // Number
passenger.end.lon                  // Number
passenger.end.insee                // String
passenger.end.literal              // String
passenger.seats                    // Number
passenger.cost                     // Number
passenger.distance                 // Number
passenger.duration                 // Number
driver.identity.firstname          // String
driver.identity.lastname           // String
driver.identity.email              // String
driver.identity.phone              // String
driver.identity.company            // String
driver.start.datetime              // Date as String
driver.start.lat                   // Number
driver.start.lon                   // Number
driver.start.insee                 // String
driver.start.literal               // String
driver.end.datetime                // Date as String
driver.end.lat                     // Number
driver.end.lon                     // Number
driver.end.insee                   // String
driver.end.literal                 // String
driver.cost                        // Number
driver.distance                    // Number
driver.duration                    // Number
```

