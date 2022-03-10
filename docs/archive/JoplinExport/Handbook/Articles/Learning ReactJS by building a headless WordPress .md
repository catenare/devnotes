---
title: Learning ReactJS by building a headless WordPress powered Site
updated: 2020-09-10 21:43:38Z
created: 2020-09-10 21:43:38Z
---

# Learning ReactJS by building a headless WordPress powered Site.
* Motivation
	* Need to redo personal site.
	* Want to experiment with front-end development especially JavaScript
	* Low-cost hosting with the ability to scale a site if necessary.
* Benefits
	* Scalability of a static site
	* Benefit of using WordPress to manage my content.
	* Completely custom front-end
* Issues
	* Everything is custom

## Getting Started
* Setting up WordPress - (WordPress with Composer)[http://composer.rarst.net]
	* Using composer, nginx and php71-fpm
		* Already know how to configure Apache. Was a good time to get more familiar with php71-fpm and nguni.
		* Setting up on my local machine. Already have php configured.
		* No desire to mess around with docker containers for this.
			* Do use docker containers for my celery and elasticsearch in development
	* Composer allows for easy configuration of local WordPress development and for upgrading the production version
		* Put everything still in development under dev dependencies
		* In production, only composer update the non-dev dependencies
		* Tools
			* Using johnbloch composer install
			* wpackagist for access to packages
			* direct access to packages via github
* Getting access to the APIs
* Benefits
	* WordPress multisite support
	* REST API including multi-site support
	* Composer support
	* Benefits of AWS
	* Use API service for cache and security
	* Use cloud services in site
	* Low cost hosting
	* Automatic CDN for front-end site
* ReCaptcha plugin support
## CSS for site
* Creating timeline via CSS