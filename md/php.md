# Wordpress Development notes
## Using sqlite as the database
* Use sqlite plugin for sqlite - [SQLite Integration](https://wordpress.org/plugins/sqlite-integration/)
* Use for lightweight development.

## To enable php71-apache2handler, run:
* ```cd /opt/local/apache2/modules```
* ```sudo /opt/local/apache2/bin/apxs -a -e -n php7 mod_php71.so```
