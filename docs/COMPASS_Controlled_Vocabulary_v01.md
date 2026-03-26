# COMPASS Controlled Vocabulary v01

**Document title:** COMPASS Controlled Vocabulary  
**Version:** v01  
**Application:** COMPASS

## 1. Purpose

This document captures the baseline controlled vocabulary identified from the current source schema and example values visible in the COMPASS implementation.

## 2. Scope

The following source fields behave like coded or semi-coded value sets:

- `gender`
- `patient_type`
- `visit_type`
- `priority_status`
- `diagnosis_type`
- `current_status`
- `country` (currently not normalized)

## 3. Baseline vocabulary sets

### 3.1 Patient Type

Observed / documented examples:
- `IDENTIFIED`
- `UNIDENTIFIED`
- `REFERRED`

### 3.2 Visit Type

Observed / documented examples:
- `ANC`
- `IN-PATIENT`
- `OUT-PATIENT`
- `EMERGENCY`

### 3.3 Priority Status

Observed / documented examples:
- `ROUTINE`
- `URGENT`
- `EMERGENCY`

### 3.4 Diagnosis Type

Observed / documented examples:
- `FINAL`
- `WORKING`

### 3.5 Current Status

Observed / documented examples:
- `Completed`

## 4. Known issues in v01

- `gender` values are not yet explicitly standardized.
- `country` values are not bound to a standard code system.
- capitalization rules are not yet documented.
- value definitions are not yet formally written for every coded value.

## 5. Role of v01

Controlled Vocabulary v01 serves as the baseline documented value set from which v02 improvements will be made.
