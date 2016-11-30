# MySQL Dev

Installs MySQL and configures a user and database - without relying on any of Ansible's built in `mysql_*` tasks which require `MySQLdb` to be installed on each remote host (silly).

The config defaults are designed to match a production MariaDB/Galera cluster, as [described here](http://galeracluster.com/documentation-webpages/configuration.html).

Need to provide in group vars:

```yaml
# Expected to be provided
mysql_database_name: my_database
mysql_database_user: my_user
mysql_database_user_password: some_password

# Optional
mysql_new_database_script: /home/vagrant/scripts/create_new_database.sh
```

Defaults:

```yaml
# Database
mysql_database_charset: utf8
mysql_database_collate: utf8_bin

# MySQL
mysql_default_storage_engine: InnoDB
mysql_binlog_format: ROW
mysql_query_cache_size: 0

# InnoDB
mysql_innodb_file_format: Barracuda
mysql_innodb_autoinc_lock_mode: 2
```


## Create database script

Often it's useful to be able to just reset/re-create a new database in development - we've got that covered. Just set the `mysql_new_database_script` variable and the script used to create the database will be left in that location - ready for dev use.
