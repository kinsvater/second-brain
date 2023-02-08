# Test objects in analytics database

Tools: dbt test, dbt-expectations, soda, great expectations, re_data

## Testing at the source or RAW

Test on table level:

- Number of columns, or against expected set of columns.
	- May fail due to change in schema.
	- Use meta data to count columns
- Freshness
	- E.g., if data in source ingested once a day, test last record within last 24h.
	- Use technical timestamp column, pick latest, and measure distance to now.

Test on column level:

- Uniqueness, non-null of primary keys
- Accepted values (range or set)
- Data types - can be tricky with timestamps in unexpected format

## Testing INTERMEDIATE and CORE

See [organize-analytics-db](organize-analytics-db) for meaning of INTERMEDIATE and CORE.

- Repeat same tests as in RAW.
- More sophisticated tests on CORE:
	- Duplicates (exact)
	- Duplicates (fuzzy)
	- Linkage by keys
	- 
