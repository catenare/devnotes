#Installing Postgresql with macports

 /opt/local/lib/postgresql96/bin/pg_ctl -D /opt/local/var/db/postgresql96/defaultdb -l logfile start
# postgresql96 has the following notes:
- To use the postgresql server, install the postgresql96-server port
	- postgresql96-server has the following notes:
		- To create a database instance, after install do 
			- sudo mkdir -p /opt/local/var/db/postgresql96/defaultdb
			- sudo chown postgres:postgres /opt/local/var/db/postgresql96/defaultdb
			- sudo su postgres -c '/opt/local/lib/postgresql96/bin/initdb -D /opt/local/var/db/postgresql96/defaultdb'
			- sudo mkdir -p /opt/local/var/db/postgresql96/defaultdb
			- sudo chown postgres:postgres /opt/local/var/db/postgresql96/defaultdb
			- sudo su postgres -c '/opt/local/lib/postgresql96/bin/initdb -D /opt/local/var/db/postgresql96/defaultdb'

~~sudo chmod -R 755 /opt/local/var/db/~~
~~sudo defaults write /Library/LaunchDaemons/org.macports.postgresql96-server.plist Disabled -bool false~~
~~sudo launchctl load /Library/LaunchDaemons/org.macports.postgresql96-server.plist~~
 
- sudo port load postgresql96-server
- sudo su - postgres
- /opt/local/lib/postgresql96/bin/psql -U postgres -d template1

# Setup ODBC Driver for Postgresql on Mac OS X (Excel Compatible)
* Install notes [Compiling psqlODBC on unix](https://odbc.postgresql.org/docs/unix-compilation.html)
* Install iODBC Manager from [iODBC.org](http://www.iodbc.org/dataspace/doc/iodbc/wiki/iodbcWiki/WelcomeVisitors)
    * Install Mac Version
* Download source from [Postgresql ODBC Project](https://www.postgresql.org/ftp/odbc/versions/src/)
* Untar psqlodbc source
* Build odbc driver 
	* ```./configure --with-iodbc=/usr/local/iODBC --enable-pthread```
	* ```make```
* Install driver to /usr/local/lib
	* ```sudo make Install```
    * files: psqlodbcw.so & psqlodbcw.la
* Create odbc.ini file in /etc/

```
[ODBC Data Sources]
pgdata = PostgreSQL native driver

[pgdata]
Driver      = /usr/local/lib/psqlodbcw.so
Host        = localhost
Server      = localhost
ServerName  = localhost
Database    = paseo
UserName    = paseo
Password    = paseo
Port        = 5432
Debug       = 1

[ODBC]
;Trace=1
Debug = 1
DebugFile = /tmp/odbcdebug.log
```

**This seems to work**
