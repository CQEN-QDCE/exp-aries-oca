# Intégrer le standard Overlay Capture Architecture (OCA) à l'écosystème ARIES
Voici les travaux réalisés dans le cadre d'une expérimentation visant à intégrer le standard [Overlay Capture Architecture (OCA)](https://oca.colossi.network/) à l'écosystème [ARIES](https://www.hyperledger.org/use/aries) tel que proposé dans la requête pour commentaires [ARIES RFC 0013: Overlays](https://github.com/hyperledger/aries-rfcs/blob/main/concepts/0013-overlays/README.md).

Qu'est-ce qu'OCA
Overlay Capture Architecture (OCA) est une architecture de capture de données par superposition. Elle représente un schéma comme un objet multidimensionnel composé d'une base de capture stable et de superpositions liées qui viennent enrichir la base de capture.

### Superposition de méta-informations
Une superposition de méta-informations peut être utilisé pour ajouter des informations contextuelles sur le schéma de base, notamment son nom , sa description, etc.

### Superposition d'encodage des caractères
Une superposition d'encodage des caractères peut être utilisé pour définir l'encodage du jeu de caractères (par exemple UTF-8, ISO-8859-1, Windows-1251, Base58Check, etc.). Elle peut être utile pour mettre en œuvre des solutions qui facilitent la saisie de données dans plusieurs langues.

### Superposition de format
Une superposition de format peut être utilisé pour ajouter des formats, des longueurs de champ ou des schémas de codage de dictionnaire aux attributs du schéma.

### Superposition de saisie
Une superposition de saisie peut être utilisé pour ajouter des valeurs de champ prédéfinies dans une langue spécifiée aux attributs du schéma. Pour minimiser le risque de capture de données PII imprévues, il est préférable d'éviter la mise en œuvre de champs de texte libre. Ce type de superposition permet de saisir des données structurées, ce qui élimine le risque de capturer et de stocker ultérieurement des données dangereuses.

### Superposition de libellé
Une superposition de libellé peut être utilisé pour ajouter des étiquettes dans une langue spécifique aux attributs et catégories du schéma. Ce type de superposition permet d'afficher les étiquettes dans une langue spécifique au niveau de la couche de présentation pour une meilleure compréhension par l'utilisateur final.

### Superposition d'information
Une superposition d'information peut être utilisé pour ajouter une prose pédagogique, informative ou juridique afin de faciliter le processus de saisie des données.

### Superposition d'attribut sensible

### Superposition de mise en page d'attestation
Une superposition de mise en page d'attestation peut être utilisé pour afficher les données capturées par le schéma avec, par exemple, une image de marque (_branding_). Elle permet le positionnement de texte (données et libellés), l'insertion d'images, etc. Les instructions pour définir la mise en page est un mixte de [YAML](https://yaml.org/) et de [CSS](https://fr.wikipedia.org/wiki/Feuilles_de_style_en_cascade). Le format semble propriétaire.

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

## Identifiant auto adressable (Self Addressing Identifier - SAI)
Un identifiant auto adressable est un identifiant qui est généré de manière déterministe à partir du contenu qu'il identifie et qui y est intégré, ce qui le rend, ainsi que ses données, mutuellement inviolables.

### Pour générer un SAI
1. Remplissez entièrement les données que le SAID identifiera, en laissant un espace pour la valeur du SAID lui-même.
2 .Canonicalisez les données, si nécessaire. Le résultat est appelé la base identifiable du SAID.
3. Hacher la base identifiable. Le résultat est la valeur du SAID.
4. Remplacer le caractère générique de la base identifiable par l'identifiant nouvellement généré, de sorte que le SAID soit intégré aux données qu'il identifie. Le résultat est appelé les données identifiées.

### Pour Vérifier un SAI
1. Canonicalisez les données, si nécessaire. Le résultat est une donnée saidifiée revendiquée.
2. Dans les données saidifiées revendiquées, remplacez la valeur du SAID par un espace réservé. Le résultat est la base identifiable pour le SAID.
3. Hacher la base identifiable.
4. Comparez la valeur de hachage au SAID. S'ils sont égaux, alors le SAID identifie les données saidifiées revendiquées.

https://github-wiki-see.page/m/trustoverip/acdc-tf-terms/wiki/self-addressing-identifier-%28SAID%29

Exemple de mise en page d'attestation:
P.S.: L'exemple ci-bas n'est pas fonctionnel. Il a été abrégé pour montrer uniquement les différentes instructions permettant la msie en page.
```
config:
  width: 400px
  height: 300px
pages:
  - config:
      style: \"width: 380px; height: 280px; margin: 10;\"
      background_image: SAI:zQmQg7JDptBT4CdfHuJNqfxpXf8AbvgdWes9h2731oF37ak
      name: Front
    elements:
      - type: row
        config:
          style: \"height: 30px;\"
...
                    elements:
                      - type: content
                        text: DL
                        config:
                          style: \"font-size: 14px; color: #1739ba; font-weight: bold; display: inline-block;\"
                      - type: attribute
                        name: drivingLicenseID
                        part: data
                        config:
                          style: \"display: inline-block; padding-left: 10px; text-transform: uppercase; font-size: 21px; color: #a62523;\"
...
```


# Intégration d'OCA dans Bifold
Plusieurs considérations doivent être prises en compte :
1. Quelles sont les fonctionnalités d'OCA qui nous intéressent (portéé);
2. À quel endroit on va stocker les schémas OCA;
3. Comment configurer Bifold pour retrouver le dépôt de schémas OCA;
4. Comment Bifold va appliquer le rendu des différentes couches OCA sur une attestation;

# 6.0 Résultats attendus
1. Un schéma au format _anoncred_ et une définition d'attestation associée sont enregistrées dans le registre de preuve (aka chaîne de blocs);
2. Un schéma OCA incluant une chouche de base ayant les même attributs que le schéma AnonCred, une couche superposée d'étiquettes en français-anglais et une couche superposée de mise ne page comportant un logo et un positionnement d'informations;
3. Le schéma OCA est publié dans un dépôt;
4. Une attestation, bassée sur le schéma et la définition d'attestation créé au point 1, est émise dans le porte-feuille "ARIES Mobile Agent React Native";
5. À l'affichage de l'attestation dans le porte-feuille Bifold, le schéma OCA est récupéré dans le dépôt;
6. Les libellés (nom d'attribut) de l'attestation sont remplacés par ceux définit dans les couches superposées du schéma OCA;
7. Une zone affiche, sous forme de HTML et de css, les informations définit dans la couche superposée de mise en page;

# 7.0 Analyse
L'expérimentation a permis de montrer qu'il est possible d'utiliser _OCA_ pour supporter l'internationalisation et l'affichage de l'image de marque (_branding_) d'une attestation dans le portefeuille "ARIES Mobile Agent React Native". De plus, _OCA_ offre d'autres possibilités comme l'identification des informations sensibles, l'encodage des caractères, la description d'attributs, etc. qui n'ont pas été explorées. L'intégration d'OCA dans le portefeuille a été relativement rapide étant donné que des implémentations sont déjà disponibles.

La création d'un paquet OCA est simple en utilisant l'[éditeur de schéma OCA](https://github.com/THCLab/oca-editor). Par contre, l'alignement des attributs du schéma de base avec ceux de l'_anoncred_ peut représenter une source d'erreurs. Cet outil pourrait être modifié afin d'émettre une _anoncred_ et sa définition d'attestation (_credential definition_) automatiquement dans le registre de preuve (_Indy blockchain_) lors de la publication du paquet OCA.
## 7.1 
La creation d'une superpositon pour l'affichage d'une image de marque (_CredentialOverlay_) est plus compliquée. Son format, qui inclut un mixte de YAML et de CSS, est difficile à écrire et à lire. Il est sujet à beaucoup d'erreur. Au minimum, un outil de pré-visualisation du rendu devrait être créé pour permettre de valider l'affichage avant la publication du paquet OCA dans le dépôt. Dans un monde idéal, un éditeur visuel de type _What You See - What You Get (WYSIWYG)_ serait la meilleure solution à fournir aux éventuels émetteurs dans un environnement de production. Le rendu de l'image de marque de l'attestation a été avec la composante [React Native WebView](https://www.npmjs.com/package/react-native-webview). Bien que cette dernière offre une grande compatibilité pour l'afficage d'HTML-CSS-Javascript, le rendu de l'image de marque de l,attestation est assez lent (du moins avec un émulateur de [Android Studio](https://developer.android.com/studio)). Des essais de performance plus poussés devraient être effectués pour confirmer si ce choix est judicieux.


#8.0 Conclusion
