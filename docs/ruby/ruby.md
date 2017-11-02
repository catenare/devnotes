# Ruby Notes

## RVM Notes
* Using RVM to install Ruby after upgrading OS x
    * Error message: ```dyld: Symbol not found: _clock_gettime```
    * Solution __This worked for me__: ```xcode-select --install``` - Installed command line clients from os x.
* **No GPG software exists to validate rvm-installer, skipping.**
    * Check gnupg2 installed
        * Mac OS X - `sudo port install gnupg2`
        * *Remove link to `/opt/local/bin/gpg` used to fix an earlier issue*

## Gem
* Unable to run a command from a gem when installed with *gem install*
    * Example: *gem install cocoapods*. Expect to use *pod* as a commandline client.
    * Solution: **rvm use ruby-{current}**
    * Problem related to rvm not setting up a default ruby.


 