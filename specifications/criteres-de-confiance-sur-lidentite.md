# Critères de confiance sur l’identité

{% hint style="success" %}
Les preuves de covoiturage issues des opérateurs sont classifiées selon [trois classes de confiance \(A,B,C\)](classes-de-preuve-de-covoiturage.md). Ces dernières traitent en priorité des preuves de trajets sans focalisation spécifique sur les preuves d’identité. Il y a ainsi un intérêt pour le registre, en tant que tiers de confiance, de normaliser les critères de confiance de la preuve d'identité.
{% endhint %}

### Avant-propos

La vérification de l’identité peut s’avérer d’une part lourde chez l’opérateur \(opérations, coûts, etc.\) et contraignante pour l’utilisateur. D’un autre côté, les opérateurs partenaires du registre de preuve de covoiturage entendent le besoin remonté par les collectivités territoriales souhaitant inciter le covoiturage et être rassurées quant à la fraude sur l’identité.

La complexité est ainsi de trouver un juste milieu. Le résultat présenté ci-après fait suite à l'organisation d'un atelier et plusieurs échanges asynchrones.

Aujourd’hui, le Service n’a pas pour vocation de collecter des données personnelles identifiantes telles que des pièces d’identité mais de proposer un cadre et une forme de “standardisation” de la vérification sur l’identité.

### Spécifications 

![](https://i.imgur.com/BFZk2aR.png)

#### Pièces d'identité

Les pièces d’identité considérées sont les suivantes :

* Carte Nationale d’Identité ;
* Passeport ;
* Permis de conduire ; 
* Titre de séjour ;
* Carte de transport en commun validée par l’autorité organisatrice\*.

_\*Cette disposition est uniquement valable pour les cartes de transport dont l'identité associée aura pu être contrôlée et validée par un service mis à disposition par l’autorité organisatrice \(exemple : une API de consultation de l’identité associée à un numéro de carte de transport._

{% hint style="warning" %}
Le recours à un dispositif permettant de garantir l’identité d’un utilisateur en s’appuyant sur des comptes existants pour lesquels son identité a déjà été vérifiée est également accepté. Par exemple, le recours à [France Connect](https://franceconnect.gouv.fr/) est accepté. 
{% endhint %}

#### Définitions

* **1 trajet** correspond à 1 couple passager / conducteur. \(nb : un véhicule avec 2 passagers équivaut à 2 trajets\)
* **1 flux financier conducteur.rice** équivaut à la somme réellement perçue par le conducteur \(incitations comprises\)
* **1 flux financier passager.e** équivaut à l’équivalent du prix devant être initialement payé par le passager. Les incitations sont à valoriser, par exemple si le trajet est gratuit pour le passager grâce à une prise en charge de la part de l’AOM, le flux financier correspond au prix initial.
* **1 incitation** : contrepartie financière ou non-financière distribuée par une AOM, via un opérateur de covoiturage, à des covoitureurs répondants aux critères d'une politique d'incitation.

#### A partir de quand un opérateur peut demander auprès de ses utilisateurs une pièce d'identité ?

En ce qui concerne le seuil de déclenchement de la demande de pièce d’identité celui-ci se fait à la discrétion de l'opérateur. En substance, un opérateur peut tout à fait demander les pièces d’identité dès le premier euro côté conducteur.rice ou côté passager.e. Ce qui importe c’est que cette pièce d’identité soit communiquée à compter des seuils indiqués sur le schéma ci-avant. Ceci permet notamment de prendre en compte les délais de communication d’informations de la part de l’utilisateur et les délais de validation côté opérateur.

_Exemple : un opérateur peut demander la pièce d’identité à compter du 25eme trajet côté passager.e ce qui laisse 25 trajets à ce dernier pour communiquer cette information et la faire valider par l'opérateur._

#### Je suis opérateur d'une plateforme à la fois numérique & physique ces dispositions s'appliquent-elles ?

En ce qui concerne le.a passager.e ou le conducteur.rice ces dispositions sont uniquement valables si la mise en relation s’est faite via une plateforme numérique. Ne sont pas concerné.e.s les passager.e.s et conducteur.rices de type covoiturage spontané avec l’utilisation uniquement d’une infrastructure physique \(borne ou arrêt\).

#### Que signifie "_l'opérateur valide_" ?

Il va de soi que l’opérateur s’engage, une fois une pièce d’identité en sa possession à valider la cohérence vis-à-vis de ce qui est indiqué sur la plateforme, des noms de famille ou d'usage, prénoms et date de naissance de l'utilisateur. Les détails de la méthode utilisée \(validation manuelle, prestation externalisée, etc\) par l'opérateur est à sa discrétion. Des compléments pourront être demandés en cas d'anomalie majeure détectée de la part du Service.

#### Côté conducteur.rice, que signifie _“L'utilisateur ne plus recevoir d'incitations jusqu'à la communication de la pièce d'identité_"

Il s'agit d'un blocage de la part de l'opérateur du versement de l’incitation, c’est à dire le moment où le conducteur.rice va bénéficier de l’incitation. Le.a conductreu.rice peut tout à fait continuer à covoiturer, cependant il/elle ne pourra percevoir d’incitation tant qu’une pièce d’identité n’aura pas été communiquée et validée par l’opérateur. Durant cette période, le.a conducteur.rice peut tout à fait continuer d’accumuler des gains, points, etc dans le système de capitalisation d’incitation mis en oeuvre par l’opérateur.

#### Côté passager.e, que signifie “_L'utilisateur ne plus bénéficier ou recevoir d'incitations jusqu'à la communication de la pièce d'identité_"

Il s'agit d'un blocage de la part de l'opérateur de la perception de l'incitation. Le.a passager.e peut tout à fait continuer à covoiturer, cependant il/elle ne pourra percevoir d’incitation tant qu’une pièce d’identité n’aura pas été communiquée et validée par l’opérateur. A titre d'exemple, en cas de prise en charge par l'AOM d'une partie ou de la totalité du trajet, le.a passager.e devra payer le prix initial du trajet si ce.tte dernier.e n'a pas communiqué.e sa pièce d'identité au moment désiré.

### Prochaine étape

Notre souhait d'intégrer ces bonnes pratiques aux Conditions Générales d’Utilisation dans la partie “obligations des opérateurs” est toujours d’actualité. Toutefois, après une phase de réflexion nous comprenons que la date d’application dans les CGU au 1er septembre 2020 puisse être complexe, à la vue du contexte actuel. 

Nous rappelons tout de même que les réflexions sur ce sujet ont débuté le 2 décembre 2019 lors d’un atelier réalisé à la demande de plusieurs opérateurs. 

Le nouveau calendrier est le suivant : 

* Dès à présent, nous invitons les opérateurs volontaires ayant déjà mis en oeuvre ces bonnes pratiques à se signaler. Nous échangerons alors avec eux et acterons leur compatibilité avec les spécifications susmentionnées. Les opérateurs pourront tout à fait communiquer sur le fait d'être compatible avec ces spécifications ;
* Dès à présent, nous invitons également les opérateurs volontaires souhaitant mettre en oeuvre ces bonnes pratiques à nous l’indiquer. Nous pouvons vous accompagner si jamais vous avez des questions. Attention, l’aide proposée ici ne consiste pas à vous aider techniquement dans l’implémentation de ces bonnes pratiques ;
* Symboliquement ces bonnes pratiques seront intégrées dans les Conditions Générales d’Utilisation comme une obligation de la part des opérateurs\* au 2 décembre 2020 \(un an après la première réunion\).

\*Ces obligations s’appliqueront uniquement pour les opérateurs dont le volume mensuel de trajets remontés auprès du Service est supérieur à 5 000.  


 

