# COMPASS DIS v01

**Document title:** COMPASS Data Input Schema  
**Version:** v01  
**Application:** COMPASS

## 1. Purpose

This document describes the current Data Input Schema (DIS) implemented in the COMPASS ETL repository.

## 2. Current implementation location

- `init_database.sql`

## 3. Input entities

The source schema currently contains three main tables:

- `Patient`
- `Visit`
- `Diagnosis`

## 4. Structural overview

- One **Patient** can have many **Visits**
- One **Visit** can have many **Diagnoses**

## 5. Table definitions

### Patient

| Field | Type | Definition |
|---|---|---|
| `patient_id` | `VARCHAR(10)` | Unique identifier of patient |
| `upi_number` | `VARCHAR(20)` | UPI number |
| `national_id` | `VARCHAR(20)` | National identifier |
| `first_name` | `VARCHAR(50)` | Given name |
| `last_name` | `VARCHAR(50)` | Family name |
| `gender` | `VARCHAR(10)` | Recorded gender |
| `age_years` | `INT` | Age in years |
| `age_months` | `INT` | Additional age in months |
| `phone_number` | `VARCHAR(20)` | Contact number |
| `country` | `VARCHAR(50)` | Country |
| `registration_date` | `TIMESTAMP` | Registration timestamp |
| `patient_type` | `VARCHAR(20)` | Type of patient |
| `created_by` | `VARCHAR(50)` | Creator of record |

### Visit

| Field | Type | Definition |
|---|---|---|
| `visit_id` | `VARCHAR(10)` | Unique identifier of visit |
| `patient_id` | `VARCHAR(10)` | Linked patient identifier |
| `visit_date` | `DATE` | Date of visit |
| `visit_time` | `TIME` | Time of visit |
| `visit_type` | `VARCHAR(20)` | Type of visit |
| `priority_status` | `VARCHAR(20)` | Priority level |
| `parent_visit_id` | `VARCHAR(10)` | Parent visit identifier |
| `current_status` | `VARCHAR(20)` | Visit status |

### Diagnosis

| Field | Type | Definition |
|---|---|---|
| `diagnosis_id` | `INT` | Unique diagnosis identifier |
| `visit_id` | `VARCHAR(10)` | Linked visit identifier |
| `diagnosis_type` | `VARCHAR(20)` | Type of diagnosis |
| `icd10_code` | `VARCHAR(10)` | ICD-10 code |
| `description` | `VARCHAR(100)` | Diagnosis description |
| `recorded_by` | `VARCHAR(50)` | Actor recording diagnosis |
| `recorded_at` | `TIMESTAMP` | Record timestamp |
| `is_processed` | `BOOLEAN` | ETL processing flag |

## 6. Review notes

- Several coded values are still plain strings.
- Controlled vocabularies should be made explicit.
- Sensitive personal fields should be clearly documented.
- The DIS should link to the controlled vocabulary and application data model documentation.
