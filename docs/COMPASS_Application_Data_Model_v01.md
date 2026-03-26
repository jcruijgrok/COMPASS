# COMPASS Application Data Model v01

**Document title:** COMPASS Application Data Model  
**Version:** v01  
**Application:** COMPASS  
**Team:** FAIR Data Transformation Engineers  
**Status:** Draft for review

## 1. Purpose

This document describes the current Application Data Model used by COMPASS, identifies how it is expressed in the repository, and proposes improvements based on Humanitarian Data Space (HDS) Common Data Model principles and ontology alignment.

## 2. Current implementation location

The current application data model is implemented primarily in:

- `mapping-dataset01.ttl`

Supporting implementation context appears in:

- `README.md`
- `final_ontop.py`

## 3. Current model structure

The current mapping defines three core semantic classes:

- `ex:Patient`
- `ex:Visit`
- `ex:Diagnosis`

### 3.1 Current mapped patient properties

- `ex:patientId`
- `ex:upiNumber`
- `ex:nationalId`
- `ex:firstName`
- `ex:lastName`
- `ex:gender`
- `ex:ageYears`
- `ex:ageMonths`
- `ex:phoneNumber`
- `ex:country`
- `ex:registrationDate`
- `ex:patientType`
- `ex:createdBy`

### 3.2 Current mapped visit properties

- `ex:hasPatient`
- `ex:visitDate`
- `ex:visitTime`
- `ex:visitType`
- `ex:priorityStatus`
- `ex:parentVisit`
- `ex:currentStatus`

### 3.3 Current mapped diagnosis properties

- `ex:hasVisit`
- `ex:diagnosisType`
- `ex:icdCode`
- `ex:diagnosisDescription`
- `ex:recordedBy`
- `ex:recordedAt`

## 4. Current semantic relationships

The current graph structure is:

- `Diagnosis -> hasVisit -> Visit`
- `Visit -> hasPatient -> Patient`

This is a workable semantic pattern, but it is more natural in many graph models to also expose inverse or forward-facing relations such as:

- `Patient -> hasVisit -> Visit`
- `Visit -> hasDiagnosis -> Diagnosis`

That would make querying easier and improve readability.

## 5. Assessment against HDS-style Common Data Model principles

Based on the FAIR training materials, an HDS-oriented CDM should provide:

- a shared vocabulary,
- clearly defined classes and properties,
- semantic alignment to established ontologies,
- explicit domain/range definitions,
- controlled vocabularies where appropriate,
- provenance support,
- interoperability across applications.

### 5.1 What COMPASS already does well

- It separates core entities in a modular way.
- It transforms relational data into RDF.
- It uses typed literals for integers, dates, times, and timestamps.
- It creates stable URI templates for entities.
- It expresses patient, visit, and diagnosis as separate linked resources.

### 5.2 Main gaps

- The namespace `ex:` is generic and not application- or HDS-specific.
- The mapping does not document class or property definitions.
- There are no visible `rdfs:label` or `rdfs:comment` annotations.
- Domain and range are not documented.
- There is limited alignment to established ontologies.
- Controlled vocabularies are not formalized.
- Sensitive-data and provenance semantics are not explicit enough.
- The graph currently favors ETL implementation over semantic explainability.

## 6. Proposed model improvement directions

## 6.1 Replace or supplement generic `ex:` terms with better-defined application/HDS terms

Instead of keeping only a generic example namespace, define an application namespace such as:

- `compass:`
- or an HDS-aligned namespace if one is prescribed by the programme.

### Justification
A defined namespace improves traceability, maintainability, and interoperability.

## 6.2 Add definitions for classes and properties

For each class and property, add:

- `rdfs:label`
- `rdfs:comment`
- optional `owl:equivalentClass` / `owl:equivalentProperty`
- domain/range where appropriate

### Justification
This makes the model understandable to engineers, reviewers, and downstream users.

## 6.3 Improve relationship design

Recommended additions:

- `compass:hasVisit` between patient and visit
- `compass:hasDiagnosis` between visit and diagnosis
- optional inverse properties if needed

### Justification
This improves query usability and conceptual clarity.

## 6.4 Formalize value vocabularies

Candidates for controlled values:

- gender
- patient type
- visit type
- priority status
- diagnosis type
- country codes

### Justification
Controlled vocabularies improve consistency, aggregation, and interoperability.

## 6.5 Strengthen provenance

Candidate provenance fields and semantics:

- creation actor
- recording actor
- modification timestamp
- source system
- ETL execution metadata

### Justification
Provenance is important for accountability, auditing, trust, and FAIR reuse.

## 7. Recommended ontology alignments

The table below proposes practical ontology alignments for v02. These are recommendations for review, not yet implemented facts.

| COMPASS concept | Current term | Suggested ontology alignment | Why |
|---|---|---|---|
| Patient as person | `ex:Patient` | `foaf:Person` and/or `schema:Person` | Broad interoperability for person-like records |
| Visit / encounter | `ex:Visit` | `schema:Event` as a broad fallback, or a health-specific class if later adopted | Improves reuse of event semantics |
| Diagnosis | `ex:Diagnosis` | local class plus links to ICD terminology | Keeps domain specificity while supporting coding alignment |
| country | `ex:country` | ISO country code representation, optionally `schema:Country`/place linkage | Better normalization and international interoperability |
| registration / record timestamps | `ex:registrationDate`, `ex:recordedAt` | `dct:created`, `dct:modified`, or PROV-O temporal properties where appropriate | Better metadata and provenance semantics |
| created by / recorded by | `ex:createdBy`, `ex:recordedBy` | `prov:wasAttributedTo` or a local property aligned to PROV-O | Stronger provenance modeling |
| identifiers | `ex:patientId`, `ex:upiNumber`, `ex:nationalId` | `dct:identifier` plus local subproperties where needed | Better metadata consistency |
| diagnosis code | `ex:icdCode` | local property aligned to ICD code system reference | Supports terminology interoperability |

## 8. Definitions and justifications for key entities

### 8.1 Patient
**Definition:** A person registered in the COMPASS application as a subject of care or monitoring.  
**Justification:** This is a core operational entity and should align to a widely reused person model where possible.

### 8.2 Visit
**Definition:** A healthcare-related encounter or service interaction associated with one patient at a specific date and time.  
**Justification:** This is the event-like structure that links patient context to diagnostic outcomes.

### 8.3 Diagnosis
**Definition:** A coded and/or described clinical assessment associated with a visit.  
**Justification:** This is the main outcome-oriented data object that carries ICD-linked meaning and clinical interpretation.

## 9. Suggested v02 implementation tasks

1. Introduce a non-generic namespace for the application data model.
2. Add labels, comments, and documentation for every class and property.
3. Add explicit ontology alignments where appropriate.
4. Normalize coded values into controlled vocabularies.
5. Add clearer provenance semantics.
6. Add privacy notes for sensitive person-related properties.
7. Consider adding SHACL validation shapes in a future iteration.

## 10. Suggested GitHub structure

Recommended documentation files:

- `docs/COMPASS_Data_Input_Schema_v01.md`
- `docs/COMPASS_Application_Data_Model_v01.md`

Optional future additions:

- `docs/COMPASS_CDM_Alignment_v01.md`
- `docs/COMPASS_Ontology_Alignment_v01.md`

## 11. Version history

- **v01**: First documented application data model review based on the current public COMPASS mapping and FAIR training guidance.
