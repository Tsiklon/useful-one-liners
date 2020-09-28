## Xtrabackup

### Take a backup
` # innobackupex --compress --stream=xbstream --parallel=4 /path/to/output/location `

### Take a backup - output to a single file
` # innobackupex --compress --stream=xbstream --parallel=4 /path/to/anywhere 2> /path/to/backup.log > /path/to/single/dump/file `

### extracting and preparing a backup from a single file
` # xbstream -x < /path/to/input.xbstream -C /path/to/output/directory ` - Extract the xbstream
` # innobackupex --decompress --parallel=4 /path/to/extract/with/compressed/files 2> /path/to/decompress.log ` - Decompress the compressed files - REQUIRES QPRESS
` # grep 'decompressing' /path/to/decompress.log | awk '{print $5}' | sort | uniq | xargs rm ` - remove compressed files
` # innobackupex --defaults-file=/path/to/backup-my.cnf --use-memory=(as much as can be spared)G --apply-log /path/to/mysql 2> /path/to/apply.log ` - prepare backup for import
` # chown -R mysql.mysql /path/to/mysql`
- Move old mysql data dir and log dir and create new appropriately owned log dir
- move prepared backup into place
- start mysql
-- If replica - obtain master log position and replicant user password
-- ` mysql> CHANGE MASTER to MASTER_HOST='IP', MASTER_USER='<user>', MASTER_PASSWORD='<PW>', MASTER_LOG_FILE='<log file>', MASTER_LOG_POS=<log pos>; ` - change master
-- start slave



