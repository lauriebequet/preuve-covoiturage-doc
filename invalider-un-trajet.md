---
description: Page en cours de construction
---

# Invalider un trajet

Un opérateur peut communiquer auprès du Service un trajet dans les 5 jours \(120 heures\) suivants sa réalisation. Il arrive que l'opérateur constate une anomalie ou une fraude avérée sur ce trajet après cette période et ainsi après son envoi auprès du Service. 

Grâce au point d'API présenté ci-après un opérateur peut invalider un trajet. Cette invalidation a des conséquences sur trois services du Registre : 

* Policy - Le service politique gère la mise en place de politiques d’incitation et l’application d’une politique d’incitation ;
* Certificate - service de génération et impression en PDF ou PNG des attestations de covoiturage des covoitureur.e.s ;
* Fraud - service contenant le moteur de détection d’irrégularité.

Afin de permettre aux territoires d'avoir un suivi de leur\(s\) enveloppe\(s\) et de leur\(s\) politique\(s\), un système hybride est mis en place. Les calculs d'incitation sont ainsi itérés une première fois en version provisoire "_draft_" à des fins d'affichage et une seconde fois en version complète à l'issue d'une certaine période.  

**Chronologie :**

* Envoi des trajets par l'opérateur, via API, à J+5 \(120 heures\) au plus tard ;
* Traitement de ces données pour incitation à J+5 \(120 heures\) en version "_draft_" avec des règles basiques. Ces données sont accessibles par les territoires pour prévisualiser leurs incitations ;
* Lancement du traitement fraude à J+X ;
* Itération des calculs d'incitation le 6 de chaque mois sur les données du mois précédent ;
  * Opération 1 : annulation des incitations sur les trajets invalidés ;
  * Opération 2 : application des plafonds \(exemple : 10 trajets / mois\) ; 
  * Opération 3 : restriction externe \(exemple : priorisation des campagnes sur un trajet éligible à plusieurs incitations\).
* Ouverture des points d'API "attestation" à J+X.



**A compléter et valider par John et Nico**

{% api-method method="delete" host="https://api.covoiturage.beta.gouv.fr" path="/v2/journeys/:journey\_id" %}
{% api-method-summary %}
Journey 
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="journey\_id" type="string" required=true %}
journey\_id unique envoyé dans le payload lors de la soumission du trajet
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authentication" type="string" required=true %}
Token applicatif avec la permission `journey.delete`
{% endapi-method-parameter %}
{% endapi-method-headers %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Le trajet a été invalidé.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=403 %}
{% api-method-response-example-description %}
Le token applicatif ne permet d'accéder à cette route.   
Vous pouvez en créer un nouveau dans votre interface d'administration opérateur.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Le trajet n'a pas été trouvé
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

