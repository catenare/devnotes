# Database migrations with Flyway
## Using Flyway for Migrations
* [Flyway](https://flywaydb.org/)
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

## Using with Gradle
* If using SDK - Need to use Oracle java. java 9.0.4-oracle for using with Gradle.
* Can use maven dependencies
```
buildscript {
    dependencies {
        classpath 'org.postgresql:postgresql:42.2.1'
    }
}

plugins {
    id "org.flywaydb.flyway" version "5.0.7"
}
```
* Created gradle.properties file with flyway configuration.
```
flyway.url = jdbc:postgresql://localhost:5432/paseo_dev
flyway.user = name
flyway.password = password
flyway.locations = filesystem:'migrations'
```

* Custom task to add date-timestamp to file before running migration. In build.gradle.
```
// https://stackoverflow.com/questions/43813724/gradle-script-to-append-timestamp-to-files
task renameFile {
    println(" :migrate : renameForMigration")
    def files = fileTree(dir: "${rootDir}/migrations")
    files.include '**/*.sql'
    files.exclude '**/V*.sql'
    // , include: '**/*.sql', exclude: '^V\\d+.*\\.sql')
    doLast {
        files.each{ file ->
            def newFileName = "V${getDate()}__${file.getName()}"
            ant.move(file: file, toFile:"${file.parent}/${newFileName}")
            println(newFileName)
            }
    }
}

task migrateDatabase(type: org.flywaydb.gradle.task.FlywayMigrateTask) {
    dependsOn 'renameFile'
}
```

## Notes
* Use timestamp to tag migration. Makes it easier to manage especially if you're going to be in a multi-developer environment
  * [Lessons Learned Using Flyway DB with Distributed Version Control](http://www.jeremyjarrell.com/using-flyway-db-with-distributed-version-control/)
  * Get date on mac os x command line ```date +%s ```
* Use git to track migrations - flyway notices if a migration file changes and causes issues
* Moving away from Ant - seems support is not as strong anymore.
### Tasks
* Delete public.schema_version and ran `gradle flywayBaseline` to start migrations from scratch.
