# Database migrations with Flyway
## Version control/management of updates

## Using Flyway for database version control
* Recommendations:
  * Use timestamp to tag migration. Makes it easier to manage especially if you're going to be in a multi-developer environment
    * [Lessons Learned Using Flyway DB with Distributed Version Control](http://www.jeremyjarrell.com/using-flyway-db-with-distributed-version-control/)
    * Get date on mac os x command line ```date +%s ```
  * Use git to track migrations - flyway notices if a migration file changes and causes issues
  
## Setting up flyway
* Sqlite jdbc driver - [xerial/sqlite-jdbc](https://bitbucket.org/xerial/sqlite-jdbc/downloads) - for prototyping
* Postgresql JDBC Driver - [Postgresql](https://jdbc.postgresql.org)
* Flyway ant library - [Flyway Ant](https://repo1.maven.org/maven2/org/flywaydb/flyway-ant/4.0.3/flyway-ant-4.0.3.tar.gz)
* Directory Structure
  * db
    * conf/
      * flyway.conf
    * libs/
      * flyway/ # Flyway ant
      * postgresql-9.4.1212.jar
      * ant-contrib-1.0b3.jar
    * migrations
    * build.xml
* Using the serial date for tracking migrations - ```date +%s```

## Using ant to run migrations
* Using SDKMAN to manage ant - [sdkman](http://sdkman.io) | [Ant](http://ant.apache.org/manual/index.html)
* Added Ant contrib jar
* Libs used
  * ant-contrib-1.0b3.jar  -- ant contrib jar - (Ant contrib task)[http://central.maven.org/maven2/ant-contrib/ant-contrib/1.0b3/ant-contrib-1.0b3.jar]
  * postgresql-9.4.1212.jar -- [Postgresql](https://jdbc.postgresql.org)
  * flyway - has the flyway core and ant libraries -- [Flyway Ant](https://repo1.maven.org/maven2/org/flywaydb/flyway-ant/4.0.3/flyway-ant-4.0.3.tar.gz)
  * build.xml in db library

## Deleting a migration.
### Can't delete a migration, only repair it.
1. Comment out the commands in the migration mistake you are eliminating.
1. Run ```ant repair``` to fix the checksums for the migrations
1. Validate the current tatus ```ant validate```
1. Flyway should be back to the status it is suppose to be in.