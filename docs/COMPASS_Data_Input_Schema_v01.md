# COMPASS Data Input Schema v01

**Document title:** COMPASS Data Input Schema  
**Version:** v01  
**Application:** COMPASS  
**Team:** FAIR Data Transformation Engineers  
**Status:** Draft for review and handoff to System Engineers

## 1. Purpose

This document describes the current Data Input Schema (DIS) implemented in the COMPASS ETL repository.  
The purpose of this document is to:

- identify the input data structure used by the ETL,
- make the schema explicit and versioned,
- support review and refinement by the FAIR Data Transformation Engineers,
- support handoff to the FAIR System Engineers for ETL handling.

## 2. Current implementation location

The current DIS is implemented in:

- `init_database.sql`

The schema is currently represented as a relational database schema with three core input tables:

- `Patient`
- `Visit`
- `Diagnosis`

## 3. Data Input Schema overview

The current DIS models a healthcare workflow in which:

- a **Patient** is registered,
- one patient can have one or more **Visits**,
- one visit can have one or more **Diagnoses**.

This creates the following data structure:

- `Patient (1) -> (many) Visit`
- `Visit (1) -> (many) Diagnosis`

## 4. Table definitions

### 4.1 Patient

| Field | Type | Required | Key / constraint | Definition | Notes |
|---|---|---|---|---|---|
| `patient_id` | `VARCHAR(10)` | Yes | Primary key | Unique identifier of the patient record | Core identifier in source schema |
| `upi_number` | `VARCHAR(20)` | No | — | UPI number associated with the patient | Identifier field |
| `national_id` | `VARCHAR(20)` | No | — | National identity number | Sensitive personal identifier |
| `first_name` | `VARCHAR(50)` | No | — | Patient given name | Personal data |
| `last_name` | `VARCHAR(50)` | No | — | Patient family name | Personal data |
| `gender` | `VARCHAR(10)` | No | — | Recorded gender of the patient | Currently free-text/string |
| `age_years` | `INT` | No | — | Age in completed years | Numeric demographic field |
| `age_months` | `INT` | No | — | Additional age in months | Helpful for precise age recording |
| `phone_number` | `VARCHAR(20)` | No | — | Patient phone number | Sensitive contact data |
| `country` | `VARCHAR(50)` | No | — | Country associated with patient | Could later be standardized to ISO code |
| `registration_date` | `TIMESTAMP` | No | — | Date and time of registration | Temporal metadata |
| `patient_type` | `VARCHAR(20)` | No | — | Status/category of patient | Examples in seed data: IDENTIFIED, UNIDENTIFIED, REFERRED |
| `created_by` | `VARCHAR(50)` | No | — | User or system that created the patient record | Provenance-related field |

### 4.2 Visit

| Field | Type | Required | Key / constraint | Definition | Notes |
|---|---|---|---|---|---|
| `visit_id` | `VARCHAR(10)` | Yes | Primary key | Unique identifier of the visit | Core visit identifier |
| `patient_id` | `VARCHAR(10)` | Yes | Foreign key to `Patient(patient_id)` | Identifier of the patient linked to the visit | Establishes patient-visit relation |
| `visit_date` | `DATE` | No | — | Date of visit | Temporal visit field |
| `visit_time` | `TIME` | No | — | Time of visit | Temporal visit field |
| `visit_type` | `VARCHAR(20)` | No | — | Type/category of visit | Examples in seed data: ANC, IN-PATIENT, OUT-PATIENT, EMERGENCY |
| `priority_status` | `VARCHAR(20)` | No | — | Priority/urgency level of visit | Examples: ROUTINE, URGENT, EMERGENCY |
| `parent_visit_id` | `VARCHAR(10)` | No | — | Parent visit identifier when applicable | Supports visit hierarchy or follow-up linkage |
| `current_status` | `VARCHAR(20)` | No | — | Current state of visit | Example in seed data: Completed |

### 4.3 Diagnosis

| Field | Type | Required | Key / constraint | Definition | Notes |
|---|---|---|---|---|---|
| `diagnosis_id` | `INT` | Yes | Primary key, auto-increment | Unique identifier of the diagnosis record | Technical diagnosis record key |
| `visit_id` | `VARCHAR(10)` | Yes | Foreign key to `Visit(visit_id)` | Identifier of the linked visit | Establishes visit-diagnosis relation |
| `diagnosis_type` | `VARCHAR(20)` | No | — | Type/status of diagnosis | Examples in seed data: FINAL, WORKING |
| `icd10_code` | `VARCHAR(10)` | No | — | ICD-10 diagnostic code | Should be validated against ICD-10 where relevant |
| `description` | `VARCHAR(100)` | No | — | Human-readable diagnosis description | Currently short text |
| `recorded_by` | `VARCHAR(50)` | No | — | Person or system recording diagnosis | Provenance-related field |
| `recorded_at` | `TIMESTAMP` | No | — | Date and time diagnosis was recorded | Temporal metadata |
| `is_processed` | `BOOLEAN DEFAULT FALSE` | Yes (system field) | Default flag | ETL processing status flag | Used to detect new/unprocessed diagnoses |

## 5. Structural relationships

### Relationship 1: Patient to Visit
- One patient can have multiple visits.
- This is implemented via `Visit.patient_id -> Patient.patient_id`.

### Relationship 2: Visit to Diagnosis
- One visit can have multiple diagnoses.
- This is implemented via `Diagnosis.visit_id -> Visit.visit_id`.

## 6. Current strengths of the DIS

- The schema is simple and easy to trace.
- Core entity boundaries are clear.
- The relational foreign-key structure supports ETL mapping.
- The schema includes provenance-like fields such as `created_by` and `recorded_by`.
- The schema includes temporal fields such as `registration_date`, `visit_date`, `visit_time`, and `recorded_at`.
- The `is_processed` flag supports incremental ETL.

## 7. Current limitations and review points

- Several value sets are still plain strings and are not yet documented as controlled vocabularies.
- `country` is not yet normalized to a standard code system.
- `gender` is not yet bound to a documented controlled vocabulary.
- `patient_type`, `visit_type`, `priority_status`, and `diagnosis_type` should be explicitly documented as enumerations if they are intended to be constrained.
- Sensitive fields such as names, national ID, and phone number need explicit governance and privacy notes.
- `description` may be too short for some clinical use cases if rich narrative text is needed.

## 8. Proposed next documentation improvements

For v02, add:

1. explicit allowed values for each coded field,
2. cardinality notes,
3. validation rules,
4. privacy classification by field,
5. mapping links from each source field to the application data model / CDM term.

## 9. Handoff note for System Engineers

This DIS document should be used together with:

- `init_database.sql` for the implemented source structure,
- `mapping-dataset01.ttl` for semantic transformation logic,
- `final_ontop.py` for ETL execution.

## 10. Version history

- **v01**: First documented version based on the current public COMPASS repository.
