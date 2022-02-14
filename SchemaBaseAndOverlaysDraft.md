Intro

Ce document vise à fournir une proposition de solution pour une normalisation mondiale de l'échange de données sur la base du concept de données liées. L'idée est de concevoir un schéma de base minimaliste pour les données qui pourrait être utilisé de manière très générique et de tirer parti du concept de superposition pour fournir des extensions et des fonctionnalités supplémentaires.

L'idée est que le schéma de base et les overlays soient identifiés par un identifiant décentralisé. Ce pourrait être DID si la version finale permettait de référencer tout type de contenu. Ou nous pourrions trouver une autre solution comme DRI (Decentralize Resource Identifier) qui aurait une définition beaucoup plus large que le DID actuel.

La principale raison d'avoir un identifiant décentralisé est d'attacher quelques attributs aux objets dont nous parlons :

immuabilité
interoberabilité
décentralisation
AVIS : La base de schéma n'est pas la même chose que le schéma, le schéma est créé seulement en composant la base de schéma avec les overlays.

Objets :

SCHEMA BASE OBJECT - définition du schéma de base
OVERLAY OBJECT - définition de l'overlay
SCHEMA ELEMENT OBJECT - définition de l'attribut.

#DID and DDOC vs DIDv2.0

##Context

Selon la dernière spécification (v0.11), nous pouvons utiliser un nouveau contexte dans la spécification DID. Gardez à l'esprit qu'il ne s'agit pas d'ajouter un nouveau contexte au Doc DID mais de remplacer le contexte actuel et de définir un contexte pour la base de schéma et les superpositions.

Comme pour les DID, la base de schéma et les superpositions doivent être indépendantes du réseau où elles peuvent être stockées. En suivant les mêmes règles que celles définies dans la spécification DID.

Nous pourrions exploiter le concept de contexte qui est défini dans la spécification.

L'idée serait d'utiliser un contexte dédié pour définir les objets liés au schéma afin de pouvoir étendre le modèle de données des identifiants décentralisés sans permission et de manière décentralisée.

Exemple:

    did:sov:12345xcvb # Specific Schema Base Object DID

Peut se résoudre à :
```
    {
      @context: ["https://schema-and-overlays.io/schema/v1"]
      "id": did:sov:12345xcvb
      name: "Full Name",
      description: "Person full name",
      version: "1.0",
      attr_names: {
        "first_name": did:sov:9667,
        "middle_name": did:sov:9668,
        "last_name": did:sov:9669,
      }
    }
```
Exemple:
```
    Subset overlay:
    did:sov:1234qwer123123123
```
Can resolves to:

```
    {
      @context: ["https://schema-and-overlays.io/overlay/v1"]
      "id": did:sov:123cavvbs
      attr_names: [ "first_name", "middle_name", "last_name" ]

    }
```

### DID Types

Using DID types to distinquish between did types by using dedicated schema type.
See more in [DIDSpec2.0.md](DIDSpec2.0.md) document.


## Schema Element

Schema Element represent smallest unit in schema world which is single
attribute. Schema element's are included in schema base. The idea behind schema elements is to avoid duplicates on data storage side (for example decentralize global storage or Sovrin agent) and provide universal language (semantic) for SSI ecosystem to talk between networks and data providers so we could keep compatibility between them.

Example of one element:

```
    {
      did: "did-schema-element:sov:9667",
      name: "First name",
      description: "User first name",
      version: "1.0",
    }

    {
      did: "did-schema-element:sov:668",
      name: "Middle name",
      description: "User middle name",
      version: "1.0",
    }

    {
      did: "did-schema-element:sov:9669",
      name: "Last name",
      description: "User last name",
      version: "1.0",
    }
```

## Schema Base
```
    {
      did: "did-schema:sov:66789",
      name: "Full Name",
      description: "Person full name",
      version: "1.0",
      attr_names: {
        "first_name": did-schema-element:sov:9667,
        "middle_name": did-schema-element:sov:9668,
        "last_name": did-schema-element:sov:9669,
      }
    }

    {
      did: "did-schema:sov:1234abcd",
      name: "Demographics",
      description: "Created by MEDIDATA",
      version: "1.0",
      consent: "did:schema:27312381238123", # reference to consent schema

      pii_attributes: {
        "brthd": "sensitive"
      }
      attr_names: {
        name: did:schema:666789,
        brthd: "Date",
        ...
      }


    }


CONSENT_SCHEMA = {
    did: "did-schema:27312381238123",
    name: 'Consent schema for clinical trial data',
    description: "Created by Rosche",
    version: '1.0',
    # MANDATORY KEYS
    attr_names: {
      expiration: Date,           # How long consent valid for.
      limitation: Date,           # How long data is kept.
      # Different reasons may apply. For example hold information after
      # expiration in case customer returns after some months.
      dictatedBy: String,          # Who dictates the conditions of consent,
      # Issuer / Holder. Issuer if requirement or Holder if temporary.
      # Applies to expiration & limitation
      validityTTL: Integer,       # Duration proof is valid for. Value in
    }
}

```

## Overlays

Overlays are data structure which can be applied on top of the schema base and
enrich it without need to change schema base. The purpose is to keep schema
base very generic, immutable and easily reusable. Schema base preserve context
of the data and as soon as the data would be stored, transferred or used in
credential according specific schema, you can preserve context across those
operations.

Example of overlays:

 - Entry Overlay
 - Label Overlay
 - Information Overlay
 - Encoding Overlay
 - Format Overlay (including units)
 - Source Overlay
 - Subset Overlay

 - Sensitive Overlay (filter not attached to schema base)
 - Conditional Overlay (filter on UI)

### Entry overlay

Include default values for attributes.

For example:
```
ENTRY_OVERLAY = {
  did: "did-overlay:sov:1234abcd",
  type: "spec/overlay/1.0/entry",
  name: "Demographics Entry",
  schemaDID: "did-schema:sov:3214abcd",
  schemaVersion: "1.0",
  schemaName: "Demographics",
  default_values: {
    ageUnit: ["YEAR"],
	gender: ["MALE", "FEMALE"],
	ethnicGroup: ["HISPANIC OR LATINO", "NOT HISPANIC OR LATINO", "NOT REPORTED", "UNKNOWN"],
	race2Specific: ["CHINESE", "TAIWANESE", "ASIAN INDIAN", "KOREAN", "MALAYSIAN", "VIETNAMESE", "OTHER ASIAN"]
  }
}
```
### Label Overlay

Define and label categories and add attribute labels to Schema attributes (incl. language translations)

Example:

```
LABEL_OVERLAY = {
  did: "did-overlay:sov:59248239",
  type: "spec/overlay/1.0/label",
  name: "Demographics English Labels",
  schemaDID: "did-schema:sov:3214abcd",
  schemaVersion: "1.0",
  schemaName: "Demographics",
  language: "en_US",
  attr_labels: {
    brthd: 'Date of Birth',
    ageic: 'Age',
    ageUnit: 'Age unit',
    gender: 'Sex',
    ethnicGroup: 'Ethnicity',
    indalk: 'American Indian or Alaska Native',
    asian: 'Asian',
    race2Specific: 'If race is Asian, specify origin',
    black: 'Black or African American',
    island: 'Native Hawaiian or Other Pacific Islander',
    white: 'White',
    raceunk: 'Race Unknown'
  },
  attr_categories: {
    race: [
      :indalk, :asian, :racesp,
      :black, :island, :white, :raceunk],
  },
  category_labels: {race: "Race"}
}

```

### Information Overlay

Add a layer of contextual information to a Schema (incl. procedural and/or legal prose) to better define it's expected use and/or associated terms.

For example:

```
INFORMATION_OVERLAY = {
  did: "did-overlay:sov:58kosf0239",
  type: "spec/overlay/1.0/informational",
  name: "Demographics English Informational",
  schemaDID: "did-schema:sov:3214abcd",
  schemaVersion: "1.0",
  schemaName: "Demographics",
  language: "en_US",
  attr_informations: {
    brthd: 'Fill Your Date of Birth',
    ageic: 'Fill your Age',
    gender: 'Choose your Sex',
    ethnicGroup: 'Choose your Ethnicity',
    indalk: 'Select if your are American Indian or Alaska Native',
    race2Specific: 'If race is Asian, select origin',
    black: 'Select if you are Black or African American',
    island: 'Select if you are Native Hawaiian or Other Pacific Islander',
    white: 'Select if your are White',
  },
  category_information: {race: "Select all that apply"}
}

```

### Subset Overlay

Create a Schema subset.

For example:

```
SUBSET_OVERLAY = {
	did: "did-schema:sov:1123414abcd",
  type: "spec/overlay/1.0/subset",
	name: "Demographics - Subset overlay",
	schemaDID: "did-schema:sov:3214abcd",
	schemaVersion: "1.0",
  attributes: [
      :brthd,
      :ageic,
      :ageu,
      :gender
  ]
}
```

### Sensitive Overlay

Flag personally identifiable information (PII) attributes that could unblind the identity of a person, an organization or a thing with reference to the Blinding Identity Taxonomy (BIT). It is applied on the receiver of identity request side. It serves as a extra protection layer for end customer.

For example:

```
SENSITIVE_OVERLAY = {
  did: "did-overlay:12idksjabcd",
  tyee: "spec/overlay/1.0/sensitive",
  name: "Sensitive data for private entity",
  attributes: [
      :ageic
  ]
}

```

### Encoding Overlay

Overlay which provides you information about encoding methods used to encrypt/obscure for ZKP operation. This is strongly related with the work of Verifiable Credential WG. More info soon.

For example:

```
ENCODING_OVERLAY = {
  did: "did-overlay:sov:12ide212jabcd",
  tyee: "spec/overlay/1.0/encoding",
  name: "Encoding information for data attributes",
  attributes_encoding: [
      date: "LinkedDataSignature2015"
  ]
}
```
Encoding method could be defined using security vocabulary: https://web-payments.org/vocabs/security

### Format Overlay

Overlay which carry information about data formats of the attributes like: Text, Number etc. and the units like: m, km, pounds, EUR etc.

For example:

```
FORMAT_OVERLAY = {
  did: "did-overlay:sov:12iasc212jab5",
  tyee: "spec/overlay/1.0/format",
  name: "Format information for data attributes",
  attributes_encoding: {
      date:  {:format => "ISO8601", unit: "seconds"}
      name: {format: "String"}
      weight: {format: "Decimal", unit: "kilogram"}
  }
}
```

### Conditional Overlay

Overlay which provides simple logic for presenting the data, like hide fields if are depending on another, required fields and correlation between them.

For example:

```
CONDITIONAL_OVERLAY = {
  did: "did-overlay:sov:1234abcd73",
  type: "spec/overlay/1.0/conditional",
  name: "Demographics Entry",
  schemaDID: "did-schema:sov:3214abcd",
  schemaVersion: "1.0",
  schemaName: "Demographics",
  conditional: {
    # conditional logic can be applied for attributes supported syntax:
    # :attribute_name
    # OR
    # AND
    # false
    # true
    # ==
    # !=
    # >
    # <
    # <=
    # >=
    hidden_attributes: {race2Specific: ":asian == false" },
    required_attributes: { brthd: true, gender: true, ageUnit: ":ageic != nil"}
  }
}

```

### Consent Overlay

Overlay which provides consent information for given agreement. This bit is related with work done in the Consent Receipt WG within Kantara Initiative.

For example:
```
# CONSENT OVERLAY [APPLIES IF ISSUER SETS CONDITIONS OF CONSENT]
# This applies when issuer sets explicit limits of usage. Consent is not optional.

CONSENT_RECIEPT_OVERLAY = {
  did: "did-schema:sov:5678abcd",
  type: "spec/overlay/1.0/consent_entry",
  name: "Consent receipt entry overlay for clinical trial",
  default_values: {
      expiration: "3 years",
      limitation: "2 years",
      dictatedBy: "did-key:sov:73jdu29d2", # DID of the issuer's/receiver
      validityTTL: "1 month"
      }
}

```

## Reputation

We should think of how to be able to track popularity of the schema, overlays and schema elements to measure it's reputation. So community can build up overall "standards". Probably this would be tracked via resolution where network can measure the amount of hits to specific schema or overlay. Reputation should be build outside the schema and overlay. Probably as a external system. Reputation system would be very important in the process to establish overall data normalization and unify communication language.

TOOD: challenge - how to make sure that the reputation would be valid across different network?

If we would use IPFS for storing schema and overlays we could measure reputation base on the popularity of the file - referencess on the network/pin objects.

## Predicate conditions

Allow to define overlay with simple logic to be able to apply specific predicate on any attributes.
For example:
* Are you above 18 years old? -> ( "birthdate" > 18y )
* Are you living in Poland? -> ( "address" include? 'Poland' )
* Are you citizen of Poland? -> ( "pesel" is present - PESEL is a national ID of each citizen )

This could be related with the work which is done in Verifiable Credential WG where ZKP allows you execute such operation. Multiple attributes can answer different questions, overlay could define what type of questions are supported against specific attributes. The query could be defined using ZKLang.

## TODO
* Overlay for Canonicalization Function - contains ordered graph-paths?
* Conversions?
* Transformation?
* inference - I am older then 18years old - can be done base on different verifiable credentials for example: passport, driving license (different types), national ID, or some bank accounts. All those should be valid in the context of overlay on top of the schema with specific predicates.
* ...

# Questions:
* How to deal with attributes units within overlays and schema?

  Probably it will be a good idea to keep the units out of schema to make generic schema for each use cases and let people decided in which units they want to get the data. For that purpose there will be needed unit overlay.

* Should overlay be independent?

 This would allow to reuse overlays and easily apply different overlays across schema. Good example could be BIT overlay or UNIT overlay. Others seems to be strongly tied to schema.

* How we should do categorization of schema?

  Categorization could be helpful in case if user don't know the name of the schema but want to see all schemas available from specific DID which are related with documents. For example schema to issue an invoice for that specific DID.

* How schema could be tied to specific DID?

  DID - identity could point out that he is using those specific schema for different purpose. So if someone want to communicate with him for example ask for data for issuing him an invoice he could always get the right schema. It could be done via DDOC itself or services within DDOC.



* Fingerprint of the data

Generate fingerprint of the data to be able to track who is using the data and if the consent is present.

Maybe in a form of merkel tree where we combine the attributes and as soon as we will notice a pattern within the system we can set an alert.
