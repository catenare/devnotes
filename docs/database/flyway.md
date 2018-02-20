# Using Flyway for Migrations
* [Flyway](https://flywaydb.org/)

## Notes
* Use timestamp to tag migration. Makes it easier to manage especially if you're going to be in a multi-developer environment
  * [Lessons Learned Using Flyway DB with Distributed Version Control](http://www.jeremyjarrell.com/using-flyway-db-with-distributed-version-control/)
  * Get date on mac os x command line ```date +%s ```
* Use git to track migrations - flyway notices if a migration file changes and causes issues
* Moving away from Ant - seems support is not as strong anymore.

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

## Tasks
* Delete public.schema_version and ran `gradle flywayBaseline` to start migrations from scratch.
