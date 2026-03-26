# COMPASS Workflow v01

**Document title:** COMPASS Workflow  
**Version:** v01  
**Application:** COMPASS

## Purpose

This workflow document captures the structure requested for the COMPASS documentation package after feedback from Philip.

## Workflow

The baseline documentation workflow is:

**App DIS → Controlled Vocabulary V01 → CDM V01 → Application Data Model V01 → V02 improvements**

## Meaning of each artifact

### 1. App DIS
The Application Data Input Schema (DIS) documents the source input structure used by the application and ETL.

### 2. Controlled Vocabulary V01
This documents the coded values and agreed terms used by the application at baseline.

### 3. CDM V01
This documents the Common Data Model / semantic transformation structure used to map source data into RDF.

### 4. Application Data Model V01
This documents the application-level semantic model, including classes, properties, definitions, and justifications.

### 5. V02 Improvements
This step versions the baseline documentation to improved forms after review and alignment work.

## Expected version path

- DIS v01
- Controlled Vocabulary v01
- CDM v01
- Application Data Model v01
- Controlled Vocabulary v02
- Application Data Model v02
- change log documenting the transition

## Notes for COMPASS

For the current public repository:
- DIS implementation is located in `init_database.sql`
- CDM / semantic mapping is located in `mapping-dataset01.ttl`
- ETL execution is located in `final_ontop.py`
