# Working with Amazon (AWS)

## Lightsail - virtual private server instances - $5 for 512gb instance/month
### Setting up SSH - trying to use my own ssh keys.
1. Logging in
    * Change key permissions. `chmod 600 KEYFILE`
    * `ssh -i KEYFILE ubuntu@ip-address`
### PHP Wordpress config
1. Packages
    * `php7.0 php7.0-cli php7.0-fpm php7.0-mysql php7.0-xml php7.0-mbstring php7.0-zip php7.0-gd php7.0-curl php-imagick mysql-server git nginx`
    * Install [composer](https://getcomposer.org).
        * Follow instructions from composer
    * Configure nginx and php7.0-fpm
        * nginx - configure default virtual environment
        * Enable php7.0-fpm in configuration.
    * Create rsa key to share with bitbucket or github
        * `ssh-keygen -t rsa` - no password
    * Add a deployment key to github to pull code to server.
1. Configure nginx
1. Setup mysql database
1. Download composer and wordpress command line.
    * [composer](https://getcomposer.org/)
        * `mv composer.phar /usr/local/bin/composer` after install
    * 
### Upgrading Ubuntu Service
* [How To Upgrade to Ubuntu 16.04 LTS](https://www.digitalocean.com/community/tutorials/how-to-upgrade-to-ubuntu-16-04-lts)
    * sudo do-release-upgrade -d   ;; Will upgrade to the latest LTS version in development

## Server Admin
* Restart service
    * Ubuntu
    * `sudo nginx -t` - test config
    <!--* `sudo systemctl nginx restart`-->
    * `sudo systemctl restart nginx`
    * `sudo systemctl retart php7.0-fpm`

## letsencrypt setup
* [Certbot](https://certbot.eff.org/#ubuntuxenial-nginx) - Ubuntu
* Port 443 needs to be open
* Domains need to be in nginx.conf file (sites-enabled/default) file.
* Pretty straightforward and easy to set up.

## Amazon Identity and Access Management
* Create user to access S3 and Cloudfront - will be used to upload files to S3
    * IAM Management Console
    * Create User
    * Give S3, CloudFront and APIGateway settings
## Setting up S3 and CloudFront for paseo.org.za
1. Create ssl/tls certificate
    1. Create the certificate in N. Virginia else it won't work.
    1. Make sure that you have access to one of the email addresses that Amazon will use for verification
    1. Add a domain name - *.paseo.org.za/paseo.org.za and *.martinsonline.org/martinsonline.org
1. Create S3 Bucket
    * Use basic settings. Going to use this bucket as source for CloudFront
    * Upload site with Cyberduck to s3
    * Create Bucket Policy
```json
{
    "Version": "2012-10-17",
    "Id": "Policy1488488343010",
    "Statement": [
        {
            "Sid": "Stmt1488488323316",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::barbarasierrafoothilswineries/*"
        }
    ]
}
```
1. Create CloudFront Distribution
    * Web delivery method
    * Create certificate with Certificate Manager
    * Don't forget to enter the cname record.
    * Use either both http and https or redirect http to https.
1. Update DNS records
    * Add CNAME record to dns record
        * www points to cloudfront url
1. Be sure to include root document - *index.html* - for it to work correctly.

## Issues with deployment on LightSail
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
