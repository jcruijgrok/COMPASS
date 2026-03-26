# COMPASS CDM v01

**Document title:** COMPASS Common Data Model  
**Version:** v01  
**Application:** COMPASS

## 1. Purpose

This document describes the current Common Data Model / semantic mapping as currently implemented for COMPASS.

## 2. Current implementation location

- `mapping-dataset01.ttl`

## 3. Core classes currently mapped

- `ex:Patient`
- `ex:Visit`
- `ex:Diagnosis`

## 4. Current key properties

### Patient-related
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

### Visit-related
- `ex:hasPatient`
- `ex:visitDate`
- `ex:visitTime`
- `ex:visitType`
- `ex:priorityStatus`
- `ex:parentVisit`
- `ex:currentStatus`

### Diagnosis-related
- `ex:hasVisit`
- `ex:diagnosisType`
- `ex:icdCode`
- `ex:diagnosisDescription`
- `ex:recordedBy`
- `ex:recordedAt`

## 5. Current graph structure

- Diagnosis -> Visit
- Visit -> Patient

## 6. Baseline assessment

Strengths:
- clear separation of patient, visit, and diagnosis
- RDF transformation already exists
- entity linking is implemented

Limitations:
- generic example namespace
- limited ontology alignment
- limited explicit definitions
- controlled vocabularies are not formalized in the model documentation
