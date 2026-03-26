# COMPASS ETL repository location note

## Confirmed locations in the current public repository

- **Data Input Schema (DIS):** `init_database.sql`
- **Common Data Model (CDM):** `mapping-dataset01.ttl`
- **ETL orchestration / execution:** `final_ontop.py`
- **Repository overview and usage notes:** `README.md`

## Short explanation

### Data Input Schema (DIS)
The current DIS is implemented as the relational input schema in `init_database.sql`.  
It defines the three source tables:

- `Patient`
- `Visit`
- `Diagnosis`

It also defines:
- data types
- primary keys
- foreign keys
- example data
- the `is_processed` ETL control flag in `Diagnosis`

### Common Data Model (CDM)
The current CDM is implemented in `mapping-dataset01.ttl`.  
This file defines the semantic mapping from the relational schema to RDF, including the main mapped classes and properties:

- `ex:Patient`
- `ex:Visit`
- `ex:Diagnosis`

It also defines links between them through mapping joins.

### ETL logic
The ETL pipeline is executed by `final_ontop.py`, which:
1. fetches unprocessed diagnoses from H2,
2. groups and stages visit-level data,
3. runs Ontop materialization,
4. uploads RDF to AllegroGraph,
5. marks records as processed.

## Recommended wording to share with the team

In the current COMPASS ETL repository, the **Data Input Schema (DIS)** is implemented in `init_database.sql`, the **Common Data Model (CDM)** is implemented in `mapping-dataset01.ttl`, and the ETL execution logic is implemented in `final_ontop.py`. The `README.md` gives the high-level explanation of how these components fit together.
