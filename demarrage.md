# Démarrage

## Opérateurs de covoiturage

### **Envoyer un trajet**

Envoyer un trajet de covoiturage à l’API du Registre de Preuve de Covoiturage nécessite que plusieurs critères soient remplis.

**1.**Une entité “opérateur de covoiturage” est créé sur l’application du registre.

_Nb : cette opération est réalisée par un membre de l’équipe du Registre de Preuve de Covoiturage._

**2.** Un utilisateur appartenant à cet opérateur de covoiturage est administrateur.

_Nb : la nomination du premier administrateur d’un opérateur de covoiturage est réalisée par un membre de l’équipe du Registre de Preuve de Covoiturage._

**3.** L’administrateur opérateur crée un Token applicatif JWT.

**4.** Ce Token applicatif est installé sur le serveur de l’opérateur qui va envoyer les données.

**5.** Le serveur peut communiquer avec les serveurs suivants :

1. Production : [https://api.covoiturage.beta.gouv.fr](https://api.covoiturage.beta.gouv.fr)
2. Pré-production : [https://api-staging.covoiturage.beta.gouv.fr](https://api-staging.covoiturage.beta.gouv.fr)

#### Accéder à l’application du registre

Afin de valider les critères 1 et 2, demander à votre contact au sein de l’équipe du Registre de Preuve de Covoiturage de vous créer un compte ou contactez-nous par email : [contact@covoiturage.beta.gouv.fr](mailto:contact@covoiturage.beta.gouv.fr)  


\[La procédure sera simplifiée et automatisée\]

#### Créer un Token applicatif JWT

1. Cliquer sur Tokens dans la barre latérale de l’application. Cette opération est accessible aux utilisateurs dits administrateurs d’un opérateur de covoiturage.
2. Donner un nom à l’application.
3. Copier le token généré et le conserver de manière sécurisée. Il devra être envoyé dans le header de chaque requête serveur.

  
Attention : Ce token ne pourra pas être ré-affiché ni récupéré. Si le token est perdu, il doit être recréé par la même procédure.

### **Logique de connexion au service**

Le token JWT donné lors de la création de l’application doit être envoyé dans les Headers des requêtes serveurs comme ceci :  
Authorization: Bearer {token}  


Seule la route POST /journeys/push accepte l’authentification avec ce token.

Une erreur 401 Unauthorized est retournée pour les tokens invalides.

Les tokens n’expirent pas dans le temps mais ils peuvent être mis sur une liste noire en cas d’utilisation anormale.  


Un code de retour 201 Created est retourné quand la preuve est acceptée.  


La documentation de l’API \(en cours de rédaction\) est ici :

{% embed url="https://api-staging.covoiturage.beta.gouv.fr/openapi" %}

### **Schema de trajet \(version API\)**

Plus d’informations sur : [https://hackmd.io/cg8bFxeWQQGe5Qyk4Lj7oA](https://hackmd.io/cg8bFxeWQQGe5Qyk4Lj7oA)

Les champs marqués d’un \* sont obligatoires.

| **{  journey\_id: &lt;String\|Number&gt; \*   // operator given ID  operator\_class: &lt;String&gt; \*   // type of proof \(A, B, C\)  passenger: {         identity: {          firstname: &lt;String&gt;          lastname: &lt;String&gt;          email: &lt;String&gt;          phone: &lt;String&gt; \*          company: &lt;String&gt;          over\_18: &lt;Boolean\|null&gt; // passenger is over 18 years old : true\|false\|null         }         start: {          datetime: &lt;DateTime&gt;     // UTC ISO 8601 \(YYYY-MM-DD hh:mm:ssZ\)          lat: &lt;Number&gt;            // float WGS84          lon: &lt;Number&gt;            // float WGS84          insee: &lt;String&gt;          // use String          literal: &lt;String&gt;        // human readable adresse         }         end: {          datetime: &lt;DateTime&gt;     // UTC ISO 8601 \(YYYY-MM-DD hh:mm:ssZ\)          lat: &lt;Number&gt;            // float WGS84          lon: &lt;Number&gt;            // float WGS84          insee: &lt;String&gt;          // use String          literal: &lt;String&gt;        // human readable adresse        }        seats: &lt;Number&gt;              // number of seats booked by the user \(default: 1\)        cost: &lt;Number&gt;               // cost in Euro cents ex: 10€ -&gt; 1000        distance: &lt;Number&gt;           // meters        duration: &lt;Number&gt;           // seconds  }  driver: {        identity: {          firstname: &lt;String&gt;          lastname: &lt;String&gt;          email: &lt;String&gt;          phone: &lt;String&gt; \*          company: &lt;String&gt;        }        start: {          datetime: &lt;DateTime&gt; \*   // UTC ISO 8601 \(YYYY-MM-DD hh:mm:ssZ\)          lat: &lt;Number&gt;            // float WGS84          lon: &lt;Number&gt;            // float WGS84          insee: &lt;String&gt;          // use String          literal: &lt;String&gt;        // human readable adresse        }        end: {          datetime: &lt;DateTime&gt; \*   // UTC ISO 8601 \(YYYY-MM-DD hh:mm:ssZ\)          lat: &lt;Number&gt;            // float WGS84          lon: &lt;Number&gt;            // float WGS84          insee: &lt;String&gt;          // use String          literal: &lt;String&gt;        // human readable adresse        }        cost: &lt;Number&gt;               // cost in Euro cents ex: 10€ -&gt; 1000        distance: &lt;Number&gt;           // meters        duration: &lt;Number&gt;           // seconds  } }** |
| :--- |


### **Format de trajet CSV**

Il est possible durant la phase d’expérimentation d’envoyer les données à [contact@covoiturage.beta.gouv.fr](mailto:contact@covoiturage.beta.gouv.fr) au format CSV.

Contraintes

* 1 entrée par ligne
* encodage : UTF-8
* tous les champs de type String sont entre "
* les Number ne sont pas entre guillemets: "chaine";1.123;333
* les Boolean sont littéraux: "TRUE":"FALSE"
* les Date sont au format UTC ISO 8601
* séparateur: ,
* les valeurs nulles sont vides : "chaine 1";;"valeur à gauche est nulle"
* nombre maximum de lignes par fichier: 100000
* pas de headers dans le fichier \(la première ligne contient des données\)



| **journey\_id                         // String operator\_class                     // String passenger.identity.firstname       // String passenger.identity.lastname        // String passenger.identity.email           // String passenger.identity.phone           // String passenger.identity.company         // String passenger.identity.over\_18         // Boolean passenger.start.datetime           // Date as String passenger.start.lat                // Number passenger.start.lon                // Number passenger.start.insee              // String passenger.start.literal            // String passenger.end.datetime             // Date as String passenger.end.lat                  // Number passenger.end.lon                  // Number passenger.end.insee                // String passenger.end.literal              // String passenger.seats                    // Number passenger.cost                     // Number passenger.distance                 // Number passenger.duration                 // Number driver.identity.firstname          // String driver.identity.lastname           // String driver.identity.email              // String driver.identity.phone              // String driver.identity.company            // String driver.start.datetime              // Date as String driver.start.lat                   // Number driver.start.lon                   // Number driver.start.insee                 // String driver.start.literal               // String driver.end.datetime                // Date as String driver.end.lat                     // Number driver.end.lon                     // Number driver.end.insee                   // String driver.end.literal                 // String driver.cost                        // Number driver.distance                    // Number driver.duration                    // Number** |
| :--- |




## Autorités Organisatrice de la Mobilité

En construction. 

