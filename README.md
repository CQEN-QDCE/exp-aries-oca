# Intégrer le standard Overlay Capture Architecture (OCA) à l'écosystème ARIES
Voici les travaux réalisés dans le cadre d'une expérimentation visant à intégrer le standard [Overlay Capture Architecture (OCA)](https://oca.colossi.network/) à l'écosystème [ARIES](https://www.hyperledger.org/use/aries) tel que proposé dans la requête pour commentaires [ARIES RFC 0013: Overlays](https://github.com/hyperledger/aries-rfcs/blob/main/concepts/0013-overlays/README.md).

## 1.0 Objectifs
- Comprendre le standard Overlay Capture Architecture (OCA) et ses applications possibles;
- Définir un schéma Overlay Capture Architecture (OCA) permettant la personalisation d'une attestation Indy (traduction, format de données, etc.);
- Modifier le porte-feuille [ARIES Mobile Agent React Native](https://github.com/hyperledger/aries-mobile-agent-react-native) pour qu'il affiche une attestation personnalisée;

## 2.0 Motivations
Le besoin intiale qui a mené à cette expérimentaion était de pouvoir afficher dans une forme plus lisible par un humain et par la même occasion traduire les attributs d'une attestation. Tel que décrit dans la requête pour commentaires [ARIES RFC 0043: I10n (Locali[s|z]ation)](https://github.com/hyperledger/aries-rfcs/blob/main/features/0043-l10n/README.md), le principal cas d'utilisation de DIDComm est la prise en charge du traitement automatisé, comme dans le cas des messages qui conduisent à la délivrance d'une attestation, à l'échange d'une preuve, etc. Le traitement automatisé peut être le seul moyen pour certains agents de traiter les messages, s'il s'agit de dispositifs ou de logiciels gérés par des organisations sans intervention humaine. Cependant, de nombreuses interactions requiert une intervention humaine. Par exemple, l'envoit d'une preuve à partir d'un porte-feuille mobile. C'est pourquoi, losque des humains sont impliqués, la localisation et la traduction potentielle dans diverses langues naturelles deviennent importantes. Au moment d'écrire ces lignes, le statut de la requête pour commentaires [ARIES RFC 0043: I10n (Locali[s|z]ation)](https://github.com/hyperledger/aries-rfcs/blob/main/features/0043-l10n/README.md) est "Démontrée" mais elle n'a pas encore été implémentée. Comme le standard [Overlay Capture Architecture (OCA)](https://oca.colossi.network/) offre la possibilité de créer une ou plusieurs couches personalisées d'étiquettes pour les attributs du schéma et beaucoup plus encore,cela rendait cette expérimentation encore plus profitable à essayer.

## 3.0 Environnement d\'expérimentation

### Construit avec
* [ReactNative](https://reactnative.dev/)

### Prérequis

* [npm](https://www.npmjs.com)
* [CANdy-Dev-Network](https://candy-dev.cloudcompass.ca/)
* Un téléphone ([iPhone](https://www.apple.com/ca/iphone) ou Android) ou [Android Studio](https://developer.android.com/studio)

### Facultatifs

* [VSCode](https://code.visualstudio.com)

### Installation
Suivre les instructions d'installation de la version [CQEN-QDCE](https://github.com/CQEN-QDCE) du porte-feuille "ARIES Mobile Agent React Native". Utiliser la branche "[poc-oca](https://github.com/CQEN-QDCE/aries-mobile-agent-react-native/tree/poc-oca)" pour récupérer le code de l'expérimentation.


### 3.1 Conditions initiales et prémisses

## 4.0 ???

Pour cette expérimentation, il a été décidé de minimiser les modidifications à l'attestation pour lui associer un schéma OCA. Deux options semblaient possibles: 1-Ajouter une référence (SAI) vers le schéma OCA dans un attribut de l'attestation 2-Utiliser l'identifiant unique de la définition de l'attestation (Credential Definition) pour le récupérer. La deuxième option a été choisi. Elle a l'avantage de ne pas modifier l'attestation. Par contre, une référence (SAI) permettrait de créer un lien fort entre l'attestation et son schéma OCA. La référence pourrait également être le hash du schéma OCA. Il serait ainsi impossible de le modifier. 

Le schéma de l'attestation utilisé pour l'expérimentation est:
```json
{
  "schema_name": "QCPERSON",
  "schema_version": "1.0",
  "attributes": [
    "first_name",
    "last_name",
    "birth_date",
    "street_address",
    "city",
    "province",
    "country",
    "postal_code",
    "issued"
  ]
}
```
Il est disponible sur le registre de preuve [CANdy-Dev-Network](https://candy-dev.cloudcompass.ca/). Son identifiant est Ep31SvFAetugFPe5CGzJxt:2:QCPERSON:1.0. La définition d'attestation utilisée est Ep31SvFAetugFPe5CGzJxt:3:CL:25458:QCPERSON2.

Création de schéma OCA

Un [éditeur de schéma OCA](https://github.com/THCLab/oca-editor) est disponible sur le GitHub de [The Humain Colossus Lab](https://github.com/THCLab). En plus de permettre la création de schéma OCA et offre la possibilité de les publier dans un [dépôt commun](https://repository.oca.argo.colossi.network).

Le schéma OCA [schéma OCA de l'expérimentation](https://repository.oca.argo.colossi.network/api/v4/schemas/E0ttcf4zZhRiTkazvq8X4T69q3hzug6t8zR8mAaMCe1U) inclut deux couches de libellés, une en français et une en anglais. Une couche de format est également incluse pour personaliser les attributs "birth_date" et "issued". Les noms d'attribut de la couche de base sont les mêmes que ceux de l'attestation afin d'appliquer les différentes personalisation correctement.
