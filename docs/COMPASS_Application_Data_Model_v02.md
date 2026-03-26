# COMPASS Application Data Model v02

**Document title:** COMPASS Application Data Model  
**Version:** v02  
**Application:** COMPASS

## 1. Purpose

This version improves the baseline application data model by incorporating clearer controlled vocabularies, stronger definitions, and better interoperability choices.

## 2. Main improvements from v01

- clearer terminology and versioning
- stronger relation between DIS, controlled vocabulary, and semantic model
- improved ontology alignment proposals
- more explicit justification for classes and properties
- cleaner coded value handling

## 3. Refined entities

### Patient
A person receiving care, observation, or registration in the application.

### Visit
A time-bound care interaction or clinical encounter involving one patient.

### Diagnosis
A clinical interpretation or coded diagnostic statement associated with a visit.

## 4. Refined relationships

Recommended forward-facing relations:
- `compass:hasVisit`
- `compass:hasDiagnosis`

Recommended provenance relation:
- link recording or creation actors using a provenance-oriented property

## 5. Proposed ontology alignment

| Local concept | Proposed alignment | Reason |
|---|---|---|
| Patient | `foaf:Person` and/or `schema:Person` | broad reuse and interoperability |
| Visit | `schema:Event` as broad fallback | event-like encounter semantics |
| identifiers | `dct:identifier` | reusable identifier pattern |
| creator / recorder | PROV-O aligned property | stronger provenance support |
| dates / times | typed literals plus metadata properties | clearer temporal semantics |

## 6. Controlled vocabulary dependency

v02 depends on Controlled Vocabulary v02 to ensure consistent values for:
- patient type
- visit type
- priority status
- diagnosis type
- current status
- country normalization work
