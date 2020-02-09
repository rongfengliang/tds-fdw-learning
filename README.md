# tds_fdw pgspider

## Usage

```code

CREATE EXTENSION tds_fdw;
CREATE SERVER mssql_svr
	FOREIGN DATA WRAPPER tds_fdw
	OPTIONS (servername 'db', port '1433', database 'appdemos');

CREATE USER MAPPING FOR postgres
	SERVER mssql_svr 
	OPTIONS (username 'sa', password 'Dalong!123%');

CREATE FOREIGN TABLE mssql_table (
	id integer,
	age integer,
    name varchar)
	SERVER mssql_svr
	OPTIONS (table_name 'dbo.apps', row_estimate_method 'showplan_all');
or  import schema:

IMPORT FOREIGN SCHEMA dbo
	FROM SERVER mssql_svr
	INTO public
	OPTIONS (import_default 'true');


```