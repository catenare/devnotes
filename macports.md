Installing Postgresql with macports

To create a database instance, after install do
 sudo mkdir -p /opt/local/var/db/postgresql96/defaultdb
 sudo chown postgres:postgres /opt/local/var/db/postgresql96/defaultdb
 sudo su postgres -c '/opt/local/lib/postgresql96/bin/initdb -D /opt/local/var/db/postgresql96/defaultdb'

 /opt/local/lib/postgresql96/bin/pg_ctl -D /opt/local/var/db/postgresql96/defaultdb -l logfile start
