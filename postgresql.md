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

# Allowing remote setup on Mac OS X installed via MacPorts
- Config files are in */opt/local/var/db/postgresql96/defaultdb*
- ```sudo su postgres``` to edit the files
- Edit pg_hba.conf - ```host all all 192.168.1.0/24 trust``` to allow local network access
- Edit postgresq.conf - Under listen and settings - ```listen_address = "*"``` will allow network access.
- sudo port unload postgresql96-server
- sudo port load postgresql96-server
- configure Mac OS X firewall to allow remote access
## Open a port on Mac OS X
- [Open a port on mac os x](https://gauravsohoni.wordpress.com/2015/04/14/mac-osx-open-port/)
- Edit /etc/pf.conf
- Add line ```pass in proto tcp from any to any port 5432```
- Restart firewall ```sudo pfctl -f /etc/pf.conf```
## Access database consistently
- Create entry in ```/etc/hosts```
- Remote entry ```192.168.1.103    paseodb```
- Local entry  ```127.0.0.1 	   paseodb```
- Will allow access without having to manually change settings everytime.

# Setup ODBC Driver for Postgresql on Mac OS X (Excel Compatible)
* Install notes [Compiling psqlODBC on unix](https://odbc.postgresql.org/docs/unix-compilation.html)
* Install iODBC Manager from [iODBC.org](http://www.iodbc.org/dataspace/doc/iodbc/wiki/iodbcWiki/WelcomeVisitors)
    * Install Mac Version
* Download source from [Postgresql ODBC Project](https://www.postgresql.org/ftp/odbc/versions/src/)
* Untar psqlodbc source
* Build odbc driver 
	* ```./configure --with-iodbc=/usr/local/iODBC --enable-pthreads```
	* ```make```
* Install driver to /usr/local/lib
	* ```sudo make Install```
    * files: psqlodbcw.so & psqlodbcw.la
* ~~Create odbc.ini file in /etc/~~
* Create *odbc.ini* and *odbcinst.ini* files in */Library/ODBC*
* Copied */usr/local/lib/psqlodbcw.so* and */usr/local/lib/psqlodbcw.la* to */Library/ODBC/ODBCDataSources*
	* Allowed to load driver from excel.

odbcinst.ini

```
[PostgreSQL]
Description=ODBC For Postgresql
Driver=/Library/ODBC/ODBCDataSources/psqlodbcw.so

[ODBC]
Trace=1
Debug=1
```

odbc.ini

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
