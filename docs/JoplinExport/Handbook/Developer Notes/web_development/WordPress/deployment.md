---
title: deployment
updated: 2020-09-10 22:07:13Z
created: 2020-09-10 22:07:13Z
---

# Wordpress deployment notes
## Deploying the site
### Backend Code - Wordpress Code
1. Create tag of current site in master
    * `git checkout master`
    * `git tag -a v1.0 -m "Initial version of site launched"`
    * `git push origin --tags`
1. Merge code to master.
    * `git checkout master`
    * `git merge dev`
    * `git push origin`
1. Deploy backend code to server
    * `ssh -i keyfile.pem {user}@{server}`
    * Update server: 
        * `sudo apt-get update`
        * `sudo apt-get upgrade -y`
    * Access the correct folder
        * `/path/to/wordpress/folder`
        * `git pull origin master`
    * Run composer update without dev.
        * `composer update --no-dev -vvv` - no dev packages and verbose.
1. Login and activate plugins.
1. Test API access.

### Issues with deployment
* Error *PHP Fatal error: Uncaught exception 'ErrorException' with message 'proc_open(): fork failed - Cannot allocate memory' in phar*
    * [proc-open-fork-failed-errors for details](https://getcomposer.org/doc/articles/troubleshooting.md#proc-open-fork-failed-errors for details)
```bash
/bin/dd if=/dev/zero of=/var/swap.1 bs=1M count=1024
/sbin/mkswap /var/swap.1
/sbin/swapon /var/swap.1
```
* Add Permanent swap [Add swap to Ubuntu](https://www.digitalocean.com/community/tutorials/how-to-add-swap-on-ubuntu-14-04)
## Adding API Theme
* Adding a public theme to show when hitting the front page of our api.
