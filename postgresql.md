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