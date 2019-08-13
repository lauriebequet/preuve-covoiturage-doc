# Alimenter le registre via l'API

Voir également [Schema JSON](../api/schema-json.md).

Envoyer un trajet de covoiturage à l’API du Registre de Preuve de Covoiturage nécessite que plusieurs critères soient remplis.

* 1️⃣ Une entité “**opérateur de covoiturage**” est créée sur l’application du registre.
* 2️⃣ Un utilisateur appartenant à cet opérateur de covoiturage est **administrateur**.
* 3️⃣ L’administrateur opérateur **crée un Token applicatif JWT**.
* 4️⃣ Ce Token applicatif est **installé sur le serveur de l’opérateur** qui va envoyer les données et sera passé dans le _Header_ de chacune des requêtes.
* 5️⃣ Le serveur peut **communiquer** avec les serveurs suivants :
  1. Production : [https://api.covoiturage.beta.gouv.fr](https://api.covoiturage.beta.gouv.fr)
  2. Pré-production : [https://api-staging.covoiturage.beta.gouv.fr](https://api-staging.covoiturage.beta.gouv.fr)

### 1️⃣ 2️⃣ - Accéder à l’application du registre <a id="docs-internal-guid-1dcfb04d-7fff-6cd0-6f9f-785ab6cd35bb"></a>

Afin de valider les critères 1️⃣ et 2️⃣, veuillez à respecter la procédure [Rejoindre le registre](onboarding.md). En effet, ces opérations sont réalisées par un membre de l’équipe du Registre de Preuve de Covoiturage.

> La procédure sera simplifiée et automatisée.

### 3️⃣ - Créer un Token applicatif JWT

Cette manipulation est réalisable, uniquement pour les utilisateurs dits administrateurs, sur l'interface applicative du Registre de Preuve de Covoiturage. 

1. Créer un nouveau token ;
2. Donner un nom à ce token ; 
3. Copier le token généré et le conserver de manière sécurisée. **Il devra être envoyé dans le header de chaque requête serveur.**

{% hint style="danger" %}
Ce token ne pourra pas être ré-affiché ni récupéré. Si le token est perdu, il doit être recréé par la même procédure.
{% endhint %}

### 4️⃣5️⃣ - Logique de connexion au service

Le token JWT donné lors de la création de l’application doit être envoyé dans les Headers des requêtes serveurs comme ceci :

`Authorization: Bearer {token}`

Seule la route `POST /journeys/push` accepte l’authentification avec ce token.  
Une erreur `401 Unauthorized` est retournée pour les tokens invalides.  
Un code de retour `201 Created` est retourné quand la preuve est acceptée.

{% hint style="info" %}
Les tokens n’expirent pas dans le temps mais ils peuvent être mis sur une liste noire en cas d’utilisation anormale.
{% endhint %}

## Foire Aux Questions 

### Qu'est-ce qu'un trajet ?

Dans la base de données les trajets correspondent à des couples passager-conducteur contenant les informations d'un trajet effectué. Ainsi si dans un covoiturage le nombre de passager est de 2 alors deux couples sont envoyés au registre : 

* Conducteur 1 - Passager 1 : 10 km, etc. 
* Conducteur 1 - Passager 2 : 10,5 km, etc. 

### Quel est le délai d'envoi des preuves de covoiturage ? 

Le registre a pour vocation d'agréger des preuves de covoiturage notamment dans l’objectif de lutter contre la fraude massive. Cette preuve de covoiturage est constituée d’un point de départ et d’arrivée. En conséquence, il n’est pas possible, aujourd’hui, pour le registre de délivrer des attestations de covoiturage, pendant un trajet afin d’obtenir une incitation en temps réel. En revanche, il est indispensable pour les organismes incitateurs d’obtenir des informations sur la réalisation d’un trajet au plus vite. En conséquence, un juste milieu doit être trouvé.

Le consensus trouvé avec les différentes parties prenantes est un délai de 5 jours \(120 heures\) entre la fin du trajet et la communication de la preuve de covoiturage. Nos processus de contrôle opérant durant 2 jours \(48H00\), notre promesse serait “retrouvez dans le registre de preuve de covoiturage, les trajets réalisés en maximum une semaine”.

![Temporalit&#xE9; du parcours d&apos;une preuve de covoiturage.](https://lh3.googleusercontent.com/zKrEFxQ9BVpbDk2xWzorif1mu5Zm_6n6sarxLR1RDx9GDTpLN2GiLhenyjPw0-twOk9B5y7zY8hdmvkMy1fPP0cFLgBZlIvqG7RcDaxjunevmWX8w1uNxqaxdarVLO6ReK_w2uSn)

### Peut-on envoyer des preuves de covoiturage versionnées sur le registre ? 

A l’heure actuelle, il n’est pas possible de modifier une preuve soumise au registre. C’est une évolution possible que nous étudions. Nous publierons très probablement un document sur le sujet avec la base de nos réflexions et vous inviterons à l’amender avec vos propositions et remarques.  




