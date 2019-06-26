# Schema CSV

Pour alimenter le registre avec des données en format CSV, voir également "[alimenter le registre via des tableurs](../mode-demploi/alimenter-le-registre-via-des-tableurs.md)".

Nb : Il est possible durant la phase d’expérimentation d’envoyer les données à [contact@covoiturage.beta.gouv.fr](mailto:contact@covoiturage.beta.gouv.fr) au format CSV.

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

Note ¹ : les champs de position sont requis de la manière suivante : lat/lon **OU** insee **OU** literal.

```text
journey_id                                 // String <required|unique>
operator_journey_id                        // String
operator_class                             // String <required : A, B, C>
passenger.identity.firstname               // String
passenger.identity.lastname                // String
passenger.identity.email                   // String
passenger.identity.phone                   // String <required>
passenger.identity.company                 // String
passenger.identity.over_18                 // Boolean
passenger.identity.travel_pass.name        // String
passenger.identity.travel_pass.user_id     // String
passenger.start.datetime                   // Date as String <required>
passenger.start.lat                        // Number <required ¹>
passenger.start.lon                        // Number <required ¹>
passenger.start.insee                      // String <required ¹>
passenger.start.literal                    // String <required ¹>
passenger.start.country                    // String <required ¹>
passenger.end.datetime                     // Date as String <required>
passenger.end.lat                          // Number <required ¹>
passenger.end.lon                          // Number <required ¹>
passenger.end.insee                        // String <required ¹>
passenger.end.literal                      // String <required ¹>
passenger.end.country                      // String <required ¹>
passenger.seats                            // Number <required>
passenger.contribution                     // Number <required>
passenger.incentives                       // String <required> serialized array of objects
passenger.distance                         // Number
passenger.duration                         // Number
driver.identity.firstname                  // String
driver.identity.lastname                   // String
driver.identity.email                      // String
driver.identity.phone                      // String <required>
driver.identity.company                    // String
driver.identity.travel_pass.name           // String
driver.identity.travel_pass.user_id        // String
driver.start.datetime                      // Date as String <required>
driver.start.lat                           // Number <required ¹>
driver.start.lon                           // Number <required ¹>
driver.start.insee                         // String <required ¹>
driver.start.literal                       // String <required ¹>
driver.start.country                       // String <required ¹>
driver.end.datetime                        // Date as String <required>
driver.end.lat                             // Number <required ¹>
driver.end.lon                             // Number <required ¹>
driver.end.insee                           // String <required ¹>
driver.end.literal                         // String <required ¹>
driver.end.country                         // String <required ¹>
driver.revenue                             // Number <required>
driver.incentives                          // String <required> serialized array of objects
driver.distance                            // Number
driver.duration                            // Number
```

