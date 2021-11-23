# Random SQL command snippets

## Basic commands
- Some basic and oft-used commands used within the `psql` client:
	- `\l` - List databases
	- `\c blah` - switch to DB named "blah"
	- `\dt` - list tables within current DB
	- `\dx` - list installed extensions

## Counting/Selecting rows
- Different ways to get a count of rows in a table, some faster and less accurate, some slower and more accurate:
	- Exact count. Slow for big tables. If writing is happening while querying, number may be outdated by the time it returns.
	`SELECT count(*) AS exact_count FROM myschema.mytable;`
	- Estimate. Extremely fast. Typically, the estimate is very close. How close depends on whether `ANALYZE` or `VACUUM` are run frequently enough (where "enough" depends on level of write activity to the table).
	`SELECT reltuples AS estimate FROM pg_class where relname = 'mytable';`
	- Safer estimate. The above ignores the possibility of multiple tables with the same name in the same DB (in different schemas). To account for that:
	 ```
		SELECT c.reltuples::bigint AS estimate
		FROM   pg_class c
		JOIN   pg_namespace n ON n.oid = c.relnamespace
		WHERE  c.relname = 'mytable'
		AND    n.nspname = 'myschema';
	```
	- A few other examples can be found here: https://stackoverflow.com/questions/7943233/fast-way-to-discover-the-row-count-of-a-table-in-postgresql
	
-  Select only the last 10 rows from a table:
`SELECT $id FROM $table ORDER BY $id DESC LIMIT 10;`
`SELECT * FROM fraud_requests ORDER BY date_added DESC LIMIT 10;`

## Backup and Restore
- Backup a database:
`mysqldump -u root -p --all-databases > alldb_backup.sql`

- Backup a database and compress the backup:
`mysqldump -u [uname] -p[pass] [dbname] | gzip -9 > [backupfile.sql.gz]`

- Restore a backup (again, specify host/-h if it's in a Docker (and will also probably need to mount a volume)):
`mysql -u [uname] -p[pass] [db_to_restore] < [backupfile.sql]>`
`mysql -u root -p -h mysql.service.consul < backupfile.sql`

## Replication
- Check that replication is happening
- On the server:
```sql
SELECT usename,application_name,client_addr,backend_start,state,sync_state FROM pg_stat_replication;

usename   | application_name |  client_addr   |         backend_start         |   state   | sync_state 
------------+------------------+----------------+-------------------------------+-----------+------------
replicator | walreceiver      | 192.168.10.132 | 2018-07-06 06:12:20.786918+03 | streaming | async
(1 row)
```
- On the client(s):
```sql
postgres=# select pg_is_in_recovery();
 pg_is_in_recovery 
-------------------
 t
 (1 row)


postgres=# select pg_last_xlog_receive_location();
 pg_last_xlog_receive_location 
-------------------------------
 0/540C1DB8


postgres=# select pg_last_xlog_replay_location();
 pg_last_xlog_replay_location 
------------------------------
 0/540C1DB8
 (1 row)

postgres=#    SELECT CASE WHEN pg_last_xlog_receive_location() = pg_last_xlog_replay_location()
                  THEN 0
                ELSE EXTRACT (EPOCH FROM now() - pg_last_xact_replay_timestamp())
              END AS log_delay;
 log_delay 
-----------
 0
 (1 row)
```
If the last query doesn't work (on some newer Postgres versions) you can still use the `SELECT pg_last_xact_replay_timestamp();` query


## Pindrop-specific
* For IVR Backups, also use --single-transaction flag and specify the (Docker) host (will probably need to mount a volume in the Docker too):

`mysqldump -u root -p -h mysql.service.consul --all-databases --single-transaction > alldb_backup.sql`
