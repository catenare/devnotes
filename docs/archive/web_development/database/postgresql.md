#Installing Postgresql with macports

~~/opt/local/lib/postgresql96/bin/pg_ctl -D /opt/local/var/db/postgresql96/defaultdb -l logfile start~~

## postgresql96 has the following notes:
- Switch postgresql96 to postgresql10
- To use the postgresql server, install the postgresql96-server port
	- postgresql96-server has the following notes:
		- To create a database instance, after install do
			- sudo mkdir -p /opt/local/var/db/postgresql96/defaultdb
			- sudo chown postgres:postgres /opt/local/var/db/postgresql96/defaultdb
			- sudo su postgres -c '/opt/local/lib/postgresql96/bin/initdb -D /opt/local/var/db/postgresql96/defaultdb'

- Select the correct postgresql server
  - `sudo port select --set postgresql postgresql10`
- sudo port load postgresql10-server
- sudo su - postgres
- /opt/local/lib/postgresql96/bin/psql -U postgres -d template1

## Allowing remote setup on Mac OS X installed via MacPorts
- Config files are in */opt/local/var/db/postgresql96/defaultdb*
- ```sudo su postgres``` to edit the files
- Edit pg_hba.conf - ```host all all 192.168.1.0/24 trust``` to allow local network access
- Edit postgresq.conf - Under listen and settings - ```listen_address = "*"``` will allow network access.
- sudo port unload postgresql96-server
- sudo port load postgresql96-server
- configure Mac OS X firewall to allow remote access
### Open a port on Mac OS X
- [Open a port on mac os x](https://gauravsohoni.wordpress.com/2015/04/14/mac-osx-open-port/)
- Edit /etc/pf.conf
- Add line ```pass in proto tcp from any to any port 5432```
- Restart firewall ```sudo pfctl -f /etc/pf.conf```
### Access database consistently
- Create entry in ```/etc/hosts```
- Remote entry ```192.168.1.103    paseodb```
- Local entry  ```127.0.0.1 	   db```
- Will allow access without having to manually change settings everytime.



## Postgresql Server on Ubuntu
* pg_hba.conf - allow remote connection and encrypted password
    * host  all  all  0.0.0.0/0  md5
* psql
    * alter user {user} encrypted password '{password}';
* `listen_addresses = '*'`

* Connecting to ssh `ssh -i key.pem -L 3333:127.0.0.1:5433 ubuntu@api.paseo.org.za`
* Connecting to server `psql -h localhost -p 3333 -U paseo -W`

### Configuring Postgresql with UUID and Postgis support.
* lookfindme setup
* Tools
  * Using [Flyway](https://flywaydb.org) and [Gradle](https://gradle.org/) for migrations.
  * Location - *lookfindmeAPI/tools/database*
* Create User and Database
    * Create User
        * `createuser lookfindme --username=lookfindme --login --no-superuser --inherit --no-replication --createdb -P`
    * Create Database with created user.
        * `createdb --owner=lookfindme -U lookfindme lookfindme 'lookfindme database'`
    * Add uuid extension
        * **Have to be superuser to install uuid extension.**
        * `* psql -d lookfindme -U lookfindme -c 'create extension "uuid-ossp" schema public;'`
     * Add postgis extension
        * `* psql -d lookfindme -U lookfindme -c 'create extension "postgis" schema public;'`
        * `* psql -d lookfindme -U lookfindme -c 'create extension "fuzzystrmatch" schema public;'`
        * `* psql -d lookfindme -U lookfindme -c 'create schema if not exists tiger;'`
        * `* psql -d lookfindme -U lookfindme -c 'create extension "postgis_tiger_geocoder" schema tiger;'`
        * `* psql -d lookfindme -U lookfindme -c 'create extension "postgis_tiger_geocoder";'` - Note: no schema.
        * `* psql -d lookfindme -U lookfindme -c 'create extension "address_standardizer";'` - Note: no schema.
* Setup Database with Docker and composer.
    * See *docker-compose.yml* for name and ports.
    * `createuser lookfindme -h localhost -p 15432 --username=lookfindme --login--no-superuser --inherit --no-replication --createdb -P`
    * `createdb -h localhost -p 15432 --owner=lookfindme -U lookfindme lookfindme 'lookfindme database'`
    * Add extensions
    * `* psql -h localhost -p 15432 -d lookfindme -U lookfindme -c 'create extension "uuid-ossp" schema public;'`
    * `* psql -h localhost -p 15432 -d lookfindme -U lookfindme -c 'create extension "postgis" schema public;'`
    * `* psql -h localhost -p 15432 -d lookfindme -U lookfindme -c 'create extension "fuzzystrmatch" schema public;'`
    * `* psql -h localhost -p 15432 -d lookfindme -U lookfindme -c 'create schema if not exists tiger;'`
    * `* psql -h localhost -p 15432 -d lookfindme -U lookfindme -c 'create extension "postgis_tiger_geocoder" schema tiger;'`
    * `* psql -h localhost -p 15432 -d lookfindme -U lookfindme -c 'create extension "postgis_tiger_geocoder";'` - Note: no schema.
    * `* psql -h localhost -p 15432 -d lookfindme -U lookfindme -c 'create extension "address_standardizer";'` - Note: no schema.
* Run Migrate
    * `gradle flywayBaseline`
    * `gradle migrate`

### Flyway Migrations Setup
* Create tables using *FlywayDB
    * Migrations in folder *lookfindmeAPI/tools/database*
    * Setup FlyWay with Gradle.
```groovy
/*
 * File created to rename migration files for flyway
 */
buildscript {
    dependencies {
        classpath 'org.lookfindmeql:lookfindmeql:42.2.1'
    }
}

plugins {
    id "org.flywaydb.flyway" version "5.0.7"
}

// flyway {
//     locations = ['filesystem:migrations']
// }

def getDate() {
    new Date().format('yyyyMMddHHmmssSSS')
}

// https://stackoverflow.com/questions/43813724/gradle-script-to-append-timestamp-to-files
task renameFile {
    println(" :migrate : renameForMigration")
    def files = fileTree(dir: "${rootDir}/migrations")
    files.include '**/*.sql'
    files.exclude '**/V*.sql'
    files.exclude '**/U*.sql'
    // , include: '**/*.sql', exclude: '^V\\d+.*\\.sql')
    doLast {
        files.each{ file ->
            def newFileName = "V${getDate()}__${file.getName()}"
            ant.move(file: file, toFile:"${file.parent}/${newFileName}")
            println(newFileName)
            }
    }
}

task migrate(type: org.flywaydb.gradle.task.FlywayMigrateTask) {
    dependsOn 'renameFile'
}
```
* Setup properties
    * **gradle.properties**
        * *flyway.locations = filesystem:/* - Explicit/full directory needed.
        * *flyway.url=jdbc:lookfindmeql://localhost:5432/lookfindme*
        * *flyway.user=*
        * *flyway.password=*

* Notes
    * *Need to add public."user" to create constraint which contains user*

### Alternate Create user and database
```sql
CREATE USER lookfindme WITH
	LOGIN
	NOSUPERUSER
	CREATEDB
	NOCREATEROLE
	INHERIT
	NOREPLICATION
	CONNECTION LIMIT -1
	PASSWORD 'xxxxxx';
COMMENT ON ROLE lookfindme IS 'User for lookfindme';
```
* Create database
```sql
-- Database: lookfindme

-- DROP DATABASE lookfindme;

CREATE DATABASE lookfindme
    WITH
    OWNER = lookfindme
    ENCODING = 'UTF8'
    LC_COLLATE = 'C'
    LC_CTYPE = 'UTF-8'
    TABLESPACE = pg_default
    CONNECTION LIMIT = -1;
```
* Install uuid extension - need superuser access
```sql
CREATE EXTENSION "uuid-ossp"
    SCHEMA public
    VERSION "1.1";
```

## Postgis - geo location processing using PostGis
* [Site](http://postgis.net/)

# Setup RDS on AWS

## lookfindmemain.cfvviq3vzuku.us-east-1.rds.amazonaws.com
<!-- * psql -d lookfindme -U lookfindme --host=lookfindmemain.cfvviq3vzuku.us-east-1.rds.amazonaws.com -c 'create extension "uuid-ossp" schema public;' -->
* psql -h lookfindmemain.cfvviq3vzuku.us-east-1.rds.amazonaws.com -d lookfindme -U lookfindme -c 'create extension "uuid-ossp" schema public;'
* psql -h lookfindmemain.cfvviq3vzuku.us-east-1.rds.amazonaws.com -d lookfindme -U lookfindme -c 'create extension "postgis" schema public;'
* psql -h lookfindmemain.cfvviq3vzuku.us-east-1.rds.amazonaws.com -d lookfindme -U lookfindme -c 'create extension "fuzzystrmatch" schema public;'
* psql -h lookfindmemain.cfvviq3vzuku.us-east-1.rds.amazonaws.com -d lookfindme -U lookfindme -c 'create schema if not exists tiger;'
* psql -h lookfindmemain.cfvviq3vzuku.us-east-1.rds.amazonaws.com -d lookfindme -U lookfindme -c 'create extension "postgis_tiger_geocoder" schema tiger;'
* psql -h lookfindmemain.cfvviq3vzuku.us-east-1.rds.amazonaws.com -d lookfindme -U lookfindme -c 'create extension "postgis_tiger_geocoder";'
* psql -h lookfindmemain.cfvviq3vzuku.us-east-1.rds.amazonaws.com -d lookfindme -U lookfindme -c 'create extension "address_standardizer";'
