# Organize analytics database

Works best with dbt.

Create base models on top of raw data:

- Call the database BASE or STAGING
- Use views instead of tables to save costs - ok due to the simplicity of transformations allowed.
- Use only simple transformations:
	- column selections
	- dtype casting
	- column rename
- No need to create separate environments since these are simple views of raw data.

Create at least two databases (environments) DEV and PROD for the more complex transformations:

- DEV is for testing.
- PROD is already validated, orchestrated (recreated on a schedule), and used downstream.

Create a database for one-off reporting and experimentation:

- E.g., a one-off report or advanced analytics experiments.
- Those queries usually are very complex - you want to utilize the OLAP capabilities and also store the SQLs for future reference.
- If automation is required, move objects to the PROD layer.

Organize schemas:

- RAW and BASE/STAGING will have the same schemas since the latter is a simplified, slightly polished version of the former.
- One schema per data source in RAW/STAGING.
- DEV and PROD should have the same schemas.
- For DEV/PROD: common organization from dbt docs into INTERMEDIATE and CORE (or FINAL)
	- INTERMEDIATE: layer on top of BASE/STAGING. 
		- Only developers will use INTERMEDIATE directly. 
		- Helps to refactor logic so that it is easier to comprehent by developers.
		- Just views should work fine here.
	- CORE: layer on top of INTERMEDIATE 
		- The final product of the analytics engineer and consumed downstream.
		- Use tables, not views, for performance reasons.


## References

- https://medium.com/towards-data-science/how-i-organize-my-snowflake-data-warehouse-996965fe51dc
