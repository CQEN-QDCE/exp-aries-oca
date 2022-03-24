# Comment utiliser la librairie Overlay Capture Architecture (OCA)
Importer les librairies OCA dans le package.json du projet
```json
...
  "oca.js-form-core": "^0.0.16",
  "oca.js-form-html": "^0.0.6"
...
```
```typescript
import type { OCA, 
              CaptureBase, 
              EntryOverlay, 
              MetaOverlay, 
              EntryCodeOverlay, 
              LabelOverlay, 
              FormLayoutOverlay, 
              InformationOverlay, 
              CredentialLayoutOverlay, 
              FormatOverlay } from 'oca.js'
```
```typescript
  const captureBase: CaptureBase = {
    attributes: {"dateOfBirth":"Date","fullName":"Text"},
    classification: "GICS:45102010", // C'est quoi cet attribut?
    pii: ["dateOfBirth","fullName"],
    type: "spec/capture_base/1.0"
  };

  const frLabelOverlay: LabelOverlay = {
    capture_base: "EPMaG1h2hVxKCZ5_3KoNNwgAyd4Eq8zrxK3xgaaRsz2M", // Comment on génère un SAI?
    type: "spec/overlays/label/1.0",
    language: "fr",
    attr_labels: {"dateOfBirth":"Date de naissance","fullName":"Nom"},
    attr_categories: ["_cat-1_","_cat-2_"],
    cat_labels: { "_cat-1_": "Catégorie 1", "_cat-2_": "Catégorie 2" },
    cat_attributes: { "_cat-1_": ["dateOfBirth"], "_cat-2_": ["fullName"]}
  };

  const enLabelOverlay: LabelOverlay = {
    capture_base: "EPMaG1h2hVxKCZ5_3KoNNwgAyd4Eq8zrxK3xgaaRsz2M",
    type: "spec/overlays/label/1.0",
    language: "en",
    attr_labels: {"dateOfBirth":"Date of birth","fullName":"Fullname"},
    attr_categories: ["_cat-1_","_cat-2_"],
    cat_labels: { "_cat-1_": "Catégorie 1", "_cat-2_": "Catégorie 2" },
    cat_attributes: { "_cat-1_": ["dateOfBirth"], "_cat-2_": ["fullName"]}
  };

  const oca: OCA = {
    capture_base: captureBase,
    overlays: [frLabelOverlay, enLabelOverlay]
  };
```
Modèle pour inclure une page HTML dans le WebView d'une app React Native.
https://github.com/DaniAkash/react-native-draftjs/blob/bc51410117d238e0f67f90e614fe11aacf41843b/index.js#L113
