# Quickly estimate the size of a MySQL backup

This should give a ballpark idea of how big a MySQL backup (mysqldump --single-transaction) will end up being (in MBs).

Useful to run before doing a backup so you can estimate how long it'll take (once the dump starts and you see how
quickly the backup file is growing).

`mysql -e 'SELECT table_schema "database", sum(data_length + index_length)/1024/1024 "size in MB" FROM information_schema.TABLES;'
