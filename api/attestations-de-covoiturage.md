---
description: Génération d'attestations pour les utilisateurs de services de covoiturage
---

# Attestations de covoiturage

{% hint style="info" %}
**Attestation sur l'honneur de covoiturage**

Cette page concerne les attestations fournies par les opérateurs de covoiturage.

Rendez-vous sur [https://attestation.covoiturage.beta.gouv.fr/](http://attestation.covoiturage.beta.gouv.fr/) pour générer votre attestation sur l'honneur.
{% endhint %}

{% hint style="warning" %}
Cette fonctionnalité est en cours de développement.  
En tant qu'opérateur de covoiturage, contactez nous si vous souhaitez y participer : [technique@covoiturage.beta.gouv.fr](mailto:technique@covoiturage.beta.gouv.fr)  
  
Merci de [créer des tickets](https://github.com/betagouv/preuve-covoiturage/issues/new) si vous rencontrez des problèmes.
{% endhint %}

{% hint style="warning" %}
La fonctionnalité de génération de PNG va être supprimée dans une prochaine mise à jour pour ne garder que l'attestation au format PDF.
{% endhint %}



## Statut de développement des fonctionnalités 

* [x] Génération de l'API par l'opérateur ;
* [x] Téléchargement d'un PDF ;
* [x] Téléchargement d'un PNG ;
* [x] Page de vérification de l'attestation en ligne \(accès public\) ;
* [ ] Envoi de meta-données pour injecter les données personnelles du covoitureur

## **Création de l’attestation**

La requête est faite par le serveur de l’opérateur et authentifiée avec un token applicatif dans les _headers_ \(même token que pour envoyer des preuves\).

Chaque appel crée un nouveau certificat même si les paramètres sont exactement les mêmes. 

{% hint style="info" %}
_Les valeurs de km ou coût ont pu changer entre deux appels._
{% endhint %}

Le token renvoyé dans la réponse permet d’identifier l’appelant lors de la génération du PDF/PNG. Il doit être envoyé dans les _headers_ de l’appel à `/v2/certificates/pdf/{uuid}` pour permettre le téléchargement direct du PDF par une application mobile sans repasser par le token applicatif du serveur.

```javascript
POST /v2/certificates
Authorization: Bearer ${application_token}

Request {
    // Paramètres obligatoires
    
    // const tz = Intl.DateTimeFormat().resolvedOptions().timeZone
    "tz": "Europe/Paris",
    "identity": {
        "phone": "+33612345678"
        // OU
        "phone_trunc": "+336123456",
        "operator_user_id": "111-222-333-4444"
    },
    
    // Paramètres optionnels
    "start_at": "2019-01-01T00:00:00Z",
    "end_at": "2019-12-31T23:59:59Z",
    // départ et arrivée par exemple. Radius de 1km
    // maximum 2 positions
    "positions": [{
        "lon": -0.557483,
        "lat": 47.682821
    }, {
        "lon": -0.952637,
        "lat": 47.452236
    }],
}

Response [201 Created] {
    "uuid": "34999a03-cfc5-463e-8d64-97af0f507004",
    "created_at": "2020-01-01T00:00:00+0100",
    "pdf_url": "{API_URL}/v2/certificates/pdf/34999a03-cfc5-463e-8d64-97af0f507004",
    "png_url": "{API_URL}/v2/certificates/png/34999a03-cfc5-463e-8d64-97af0f507004"
}

Response [204 No Content] {
    "code": 204,
    "error": "No carpools for this period"
}

// invalid application_token
Response [401 Unauthorized] {
    "code": 401,
    "error": "Unauthorized"
}

// missing permission in the application_token scope
Response [403 Forbidden] {
    "code": 403,
    "error": "Forbidden"
}

Response [404 Not Found] {
    "code": 404,
    "error": "Not Found"
}
```

## Télécharger une attestation

Une fois l’attestation créée en base \(201 created\), on peut télécharger un PDF ou un PNG en appelant l’URL renvoyée.

```javascript
GET ${response.pdf_url} OU ${response.png_url}

Request {} // objet vide

Response [200 OK] { Buffer... }

Response [401 Unauthorized] {
    "code": 401,
    "error": "Unauthorized"
}

Response [404 Not Found] {
    "code": 404,
    "error": "Not Found"
}
```

