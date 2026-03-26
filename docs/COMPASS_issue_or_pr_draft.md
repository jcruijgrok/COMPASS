# Draft GitHub issue / PR text

## Suggested title
COMPASS DIS documentation v01 and application data model alignment review

## Suggested issue body

### Summary
This work documents the current COMPASS Data Input Schema (DIS) and Application Data Model, and prepares the repository for clearer FAIR and ETL documentation.

### Deliverables
- Added `docs/COMPASS_Data_Input_Schema_v01.md`
- Added `docs/COMPASS_Application_Data_Model_v01.md`
- Identified current DIS location in `init_database.sql`
- Identified current application data model location in `mapping-dataset01.ttl`
- Documented ETL execution context in `final_ontop.py`

### Review focus
- Confirm that the documented DIS matches the intended ETL input structure
- Review whether coded fields should become controlled vocabularies
- Review ontology alignment recommendations
- Review whether the application data model should move from generic `ex:` terms to a clearer namespace

### Next steps
- Approve or adjust the v01 documentation
- Share final DIS with FAIR System Engineers
- Continue HDS CDM alignment work for v02
