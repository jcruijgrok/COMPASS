# COMPASS Controlled Vocabulary v02

**Document title:** COMPASS Controlled Vocabulary  
**Version:** v02  
**Application:** COMPASS

## 1. Purpose

This version improves Controlled Vocabulary v01 by making the value sets more explicit, more consistent, and more interoperable.

## 2. Proposed improvements from v01

- document allowed values formally
- define preferred capitalization
- distinguish display labels from stored values
- bind `country` to ISO country codes where possible
- define `gender` values using an agreed local list or external reference
- explain each value with a short definition

## 3. Proposed v02 value sets

### 3.1 Patient Type

| Stored value | Label | Definition |
|---|---|---|
| `IDENTIFIED` | Identified | Patient identity is known |
| `UNIDENTIFIED` | Unidentified | Patient identity is not known |
| `REFERRED` | Referred | Patient has been referred from another source |

### 3.2 Visit Type

| Stored value | Label | Definition |
|---|---|---|
| `ANC` | ANC | Antenatal care visit |
| `INPATIENT` | In-patient | Admitted care visit |
| `OUTPATIENT` | Out-patient | Non-admitted care visit |
| `EMERGENCY` | Emergency | Emergency care visit |

### 3.3 Priority Status

| Stored value | Label | Definition |
|---|---|---|
| `ROUTINE` | Routine | Standard priority |
| `URGENT` | Urgent | Urgent but not immediate emergency |
| `EMERGENCY` | Emergency | Immediate high-priority case |

### 3.4 Diagnosis Type

| Stored value | Label | Definition |
|---|---|---|
| `WORKING` | Working | Preliminary or provisional diagnosis |
| `FINAL` | Final | Finalized diagnosis |

### 3.5 Current Status

| Stored value | Label | Definition |
|---|---|---|
| `COMPLETED` | Completed | Visit has been completed |

## 4. Additional recommendations

- document null / unknown handling
- define whether extra local codes are allowed
- add version control notes whenever a value is added, renamed, or deprecated

## 5. Version note

This document is the improved version following the baseline vocabulary in v01.
