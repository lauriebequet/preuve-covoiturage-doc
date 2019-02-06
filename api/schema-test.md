# Format de trajet CSV

Il est possible durant la phase d’expérimentation d’envoyer les données à
[contact@covoiturage.beta.gouv.fr](mailto:contact@covoiturage.beta.gouv.fr) au format CSV.

## Contraintes

- 1 entrée par ligne
- encodage : `UTF-8`
- tous les champs de type `String` sont entre `"`
- les `Number` ne sont pas entre guillemets: `"chaine",1.123,333`
- le séparateur décimal est un point `.` (et non une virgule `,`)
- les `Boolean` sont littéraux: `"TRUE":"FALSE"`
- les `Date` sont au format _UTC ISO 8601_
- séparateur: `,`
- les valeurs nulles sont vides : `"chaine 1",,"valeur à gauche est nulle"`
- nombre maximum de lignes par fichier: 100000
- __pas__ de headers dans le fichier (la première ligne contient des données)

