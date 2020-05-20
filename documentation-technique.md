# Documentation technique

### Préambule <a id="Pr&#xE9;ambule"></a>

Ce document est un aperçu d'un point de vue technique de l'application Registre de Preuve de Covoiturage. Le focus est mis sur le backend.

**La documentation technique complète est accessible sur le** [**lien suivant**](https://hackmd.io/kpSL0ULCSoKhT0r9l-bGHw) **📖.** 

### Concepts <a id="Concepts"></a>

L’application est découpée en services de manière fonctionnelle. Chaque service forme un paquet NodeJS indépendant. L'architecture de ces services est présentée ci-après.



![](.gitbook/assets/image%20%2817%29.png)

Le **proxy** joue un rôle d’_API manager_ \(routes, auth\).  Il a vocation à moyen terme à disparaître pour être remplacé par un _reverse-proxy_ ou un _API manager_.

**Service certificate** : ce service génère et imprime en PDF ou PNG des attestations de covoiturage des usagers. Par l’intermédiaire de son opérateur, l’usager peut demander un _état des lieux_ de ses trajets de covoiturage sur une période à un instant T. Ce document est produit pour une identité et un opérateur seulement.

**Service acquisition** : ce service réalise des actions de contrôle de conformité du payload. La conformité du payload est jugée vis-à-vis du format du schéma de données \(cf : [schéma V2](https://registre-preuve-de-covoiturage.gitbook.io/produit/api/schema-json-v2) \) mais également vis-à-vis de règles de bon sens \(exemple : date de fin supérieure à date de début\). Si le payload est conforme il est envoyé et enregistré en tant que `journey` dans le service normalization. Un retour est effectué par le service auprès de l’opérateur.

👆 Nous conseillons aux opérateurs de sauvegarder les informations renvoyées par notre API dans un log.

**Service normalization** : ce service enrichie le `journey` avec diverses informations comme des codes postaux, des distances théoriques \(serveur OSRM\), la\(les\) commune\(s\) de départ et/ou arrivée, la\(les\) AOM concernée\(s\), la densité de population du territoire, etc.

**Service acquisition\_error** : ce service stocke les payloads non conformes aux schémas de données et rejetés par les services acquisition et normalization.

**Service carpool** : ce service redecoupe le `journey` \(couple passager/conducteur\) en un passager et un conducteur et affecte une clef de reconstitution.

**Service fraud** : ce service réalise des tests d’anomalies sur les données remontées \(exemple : nombre de sièges réservés égal à 6, distance 2 km pour une durée de 2H00, etc.\) et affecte une note.

**Service policy** : ce service affecte une incitation aux passagers, conducteurs des trajets éligibles à une campagne d’incitation définie dans le registre.

**Service trip** : ce service reconstitue le couple passager/conducteur en un `journey`.

