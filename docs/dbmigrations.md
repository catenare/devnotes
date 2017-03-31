# Database migrations with Flyway
## Version control/management of updates

### Using Flyway for migrations and database version control
* Getting the serial date to use in flyway migrations.
    * Get date on mac os x command line ```date +%s ```
    * Use the date rather than the version number to better control how the migrations are applied.