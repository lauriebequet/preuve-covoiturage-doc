# Envoyer des trajets

## Pré-requis

Envoyer un trajet de covoiturage à l’API du Registre de Preuve de Covoiturage nécessite que plusieurs critères soient remplis.

1. Une entité “opérateur de covoiturage” est créée sur l’application du registre. _Nb : cette opération est réalisée par un membre de l’équipe du Registre de Preuve de Covoiturage._
2. Un utilisateur appartenant à cet opérateur de covoiturage est administrateur. _Nb : la nomination du premier administrateur d’un opérateur de covoiturage est réalisée par un membre de l’équipe du Registre de Preuve de Covoiturage._
3. L’administrateur opérateur crée un Token applicatif JWT.
4. Ce Token applicatif est installé sur le serveur de l’opérateur qui va envoyer les données et sera passé dans le _Header_ de chaque requête.
5. Le serveur peut communiquer avec les serveurs suivants :
   1. Production : [https://api.covoiturage.beta.gouv.fr](https://api.covoiturage.beta.gouv.fr)
   2. Pré-production : [https://api-staging.covoiturage.beta.gouv.fr](https://api-staging.covoiturage.beta.gouv.fr)

### Accéder à l’application du registre <a id="docs-internal-guid-1dcfb04d-7fff-6cd0-6f9f-785ab6cd35bb"></a>

Afin de valider les critères 1 et 2, demandez à votre contact au sein de l’équipe du Registre de Preuve de Covoiturage de vous créer un compte ou contactez-nous par email : [contact@covoiturage.beta.gouv.fr](mailto:contact@covoiturage.beta.gouv.fr)

> La procédure sera simplifiée et automatisée

### Créer un Token applicatif JWT

1. Cliquer sur Tokens dans la barre latérale de l’application. Cette opération est accessible aux utilisateurs dits administrateurs d’un opérateur de covoiturage.
2. Donner un nom à l’application.
3. Copier le token généré et le conserver de manière sécurisée. Il devra être envoyé dans le header de chaque requête serveur.

> **Attention :** Ce token ne pourra pas être ré-affiché ni récupéré. Si le token est perdu, il doit être recréé par la même procédure.

## Logique de connexion au service <a id="docs-internal-guid-01c653b0-7fff-78df-7da5-a5a08a50e659"></a>

Le token JWT donné lors de la création de l’application doit être envoyé dans les Headers des requêtes serveurs comme ceci :

`Authorization: Bearer {token}`

Seule la route `POST /journeys/push` accepte l’authentification avec ce token.  
Une erreur `401 Unauthorized` est retournée pour les tokens invalides.  
Les tokens n’expirent pas dans le temps mais ils peuvent être mis sur une liste noire en cas d’utilisation anormale.  
Un code de retour `201 Created` est retourné quand la preuve est acceptée.  




