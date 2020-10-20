# Données financières

Dans la suite _driver_ signifie _conducteur_ et _passenger_ signifie _passager_.

## Données collectées par le Registre

{% hint style="info" %}
Le principe est de coller au plus près avec la réalité comptable \(transaction usager\) et d'avoir suffisamment d'informations pour recalculer le coût initial du trajet. Ceci afin de s'assurer du respect de la définition du covoiturage et de la bonne application des politiques incitatives gérées par le registre.
{% endhint %}

* `passenger.contribution` : Coût réel total du service pour l’occupant passager en fonction du nombre de sièges réservés **APRÈS** que toutes les possibles incitations aient été versées \(subventions employeurs, promotions opérateurs, incitations AOM, etc\).
* `driver.revenue`**\*** : La somme réellement perçue par le conducteur **APRÈS** que toutes les incitations \(subventions employeurs, promotions opérateurs, incitations AOM, etc.\), contributions des passagers aient été versées et que la commission éventuelle de l’opérateur soit prise.
* `passenger.seats`**\*** : Nombre de sièges réservés par l'occupant passager. Par défaut : 1

**Schéma des incitations** 

* `incentives` \* : Tableau reprenant la liste complète des incitations appliquées \(ordre d'application, montant, identifiant de l'incitateur\).

Par défaut, l'ordre d'application des politiques incitatives est le suivant : 

1. Territoire \(AOM, Région, etc.\) 
2. Sponsors \(incitations employeur, CE, etc.\) 
3. Opérateur \(opération promotionnelle, offres, etc.\)

## Données calculées par le Registre

Pour le conducteur \(_driver_\)

* `driver.expense` : Coût total engagé par le conducteur selon le barème kilométrique \(~~0,601 euros / km~~\) **AVANT** que toutes les possibles incitations aient été versées \(subventions employeurs, promotions opérateurs, incitations AOM, etc\).

   Seuls les kilomètres covoiturés sont pris en compte.

* `driver.remaining_fee = driver.expense - driver.revenue` : Somme restante à charge du conducteur **APRÈS** avoir perçu les contributions des passagers et que toutes les possibles incitations aient été versées \(subventions employeurs, promotions opérateurs, incitations AOM, etc\) et prise de commission éventuelle de l’opérateur.

Pour le passager \(_passenger_\)

* `passenger.expense = passenger.contribution - Σ passenger.incentive`: Coût total initial du trajet pour le passager **AVANT** que toutes les possibles incitations aient été versées \(subventions employeurs, promotions opérateurs, incitations AOM, etc\)
* `passenger.remaining_fee = passenger.contribution / passenger.seats :` Somme restante à charge du passager **APRES** que toutes les possibles incitations aient été versées \(subventions employeurs, promotions opérateurs, incitations AOM, etc\).

{% hint style="warning" %}
Contrôles effectués afin de s'assurer de ne pas avoir un bénéfice \(si trajet &gt; 15 km\)

`driver.expense - (Σ passenger.contributions) - (Σ driver.incentives)`≥ 0 ``

`passenger.expense - (Σ passenger.incentives)`≥ `0`
{% endhint %}

## Foire aux questions

### **1. Quelle représentation pour passenger.contribution et driver.revenue ?**

Le Registre a besoin du montant brut pour appliquer les incitations de l'AOM, c'est `driver.expense` et `passenger.expense`. Le montant après incitation est `driver.revenue` et `passenger.contribution`. Les incitations appliquées par les opérateurs \(sponsors, marchés, etc.\) sont appliquées sur `driver.expense` et `passenger.expense`. Le Registre n'en a pas connaissance.

### **2. Comment assurer la fiabilité des montants collectés \(passager\) et reversés \(conducteur\) ?**

Les montants \(expense, revenue, contribution\) sont stockés de manière définitive dans les différentes étapes de simulation. Les montants calculés des incitations le sont aussi. Si les politiques sont modifiées à posteriori, les montants ne sont pas recalculés et la promesse faite à l'usager final est respectée.

### **3. Comment inclure plusieurs subventions de la part d’acteurs connus ou inconnus du Registre ?**

Les subventions inconnues du Registre sont appliquées sur `driver.expense` et `passenger.expense`. Celles des AOM sont appliquées par le Registre.

### **4. Comment mettre les résultats des politiques de calcul à disposition des opérateurs afin d’assurer une égalité d’implémentation de ces politiques ?**

L'utilisation de la simulation \[_fonctionnalité nécessitant un échange d'implémentation avec les opérateurs_\] permet de calculer les incitations appliquées à un trajet, un conducteur ou un passager. Les montants calculés sont retournés en réponse de cette simulation. Les ID retournées pour les incitations permettent d'avoir plus de détails via une requête sur les service d'incitations.

