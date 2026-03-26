# COMPASS Application Data Model v01

**Document title:** COMPASS Application Data Model  
**Version:** v01  
**Application:** COMPASS

## 1. Purpose

This document describes the baseline application data model for COMPASS using the current semantic mapping.

## 2. Core entities

### Patient
A person registered in the application as a subject of care or monitoring.

### Visit
A healthcare-related encounter linked to one patient.

### Diagnosis
A coded and/or described clinical assessment linked to a visit.

## 3. Baseline relationships

- Patient has Visits
- Visit has Diagnoses

## 4. Definitions and justifications

### Patient
**Definition:** a person represented in the source system.  
**Justification:** needed to anchor demographics and identifiers.

### Visit
**Definition:** an event or encounter in which care is delivered or recorded.  
**Justification:** needed to organize time-bound patient interactions.

### Diagnosis
**Definition:** a clinical assessment connected to a visit.  
**Justification:** needed to record outcome-oriented health meaning and coding.

## 5. Baseline ontology notes

Potential future alignments:
- `foaf:Person` or `schema:Person` for patient-like semantics
- `schema:Event` as a broad fallback for visit-like semantics
- `dct:identifier` for identifiers
- `prov:wasAttributedTo` for provenance actors

## 6. Relationship to CDM

This v01 application data model is directly based on the current mapped CDM in `mapping-dataset01.ttl`.
