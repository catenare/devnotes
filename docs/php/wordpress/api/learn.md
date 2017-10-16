# Learning to use the REST API in Wordpress.

## Issues
* Learning this API is much harder than it should be.
* Biggest issue I'm running into is using the local client.
* Figuring out how to use the remote endpoints seems so much simpler.
* Documentation is very spotty.
* Hard to fine relevant or up-to-date resources.
* Don't seem to be many books around (that are up to date).

## Resources
* [Rest Developer Handbook](https://developer.wordpress.org/rest-api/)
* [WP Rest API Docs](http://v2.wp-api.org/)
* [WP JavaScript Client](http://v2.wp-api.org/extending/javascript-client/) - *wp-api*
    * This gets briefly mentioned in the documentation.
    * Hard to find good documentation or examples about it.

## Tools/packages used
* [Timber](https://github.com/timber/timber) - Templating engine. Not really necessary but think can be used to customize the admin site.
* [Vuejs](https://vuejs.org/) - Front-end framework I'm using for custom site.

### Other Resources
* [Node WPAPI](https://github.com/WP-API/node-wpapi) - Wordpress Node Client. - See how they are doing things.
* [ADAM SILVERSTEIN](http://www.tunedin.net/) from [10UP](https://10up.com/about/#employee-adam-silverstein) - Listened to his talks about backbonejs. Learned about wp-api that way.
    * [YouTube Put A Little Backbone in your Wordpress](https://www.youtube.com/watch?v=dRLFTpAqdb0)

## Info that helped
1. Built complete front-end client in Vuejs. 
    * Access the REST API without trying to conform to Wordpress idiosyncrasies.
1. Learn to use Promises.
1. Use TypeScript because JavaScript is all over the place.
1. Don't worry about backwards compatibility.
1. Learn how to create an admin page in Wordpress using JavaScript
    * [Create JavaScript Settings Page Using Wordpress REST API](https://torquemag.io/2017/06/creating-wordpress-settings-page-using-wordpress-rest-api/)
    * Most documentation pointing to admin-ajax.php client.

## Project
* Background
    * Need a website for the church, daycare & preschool and family.
    * Wanted to use inexpensive hosting and put together mostly static websites.
    * Want to be able to have non-developers add/update content without me being involved.
* Why Wordpress?
    * REST-API was huge selling point.
        * Static sites I can host in Amazon S3 with CloudFront for CDN
        * Basic VPS from Amazon for $5/month.
    * Simpler overall API than Drupal. Having done Drupal development, just seemed a little more focused.
    * Didn't want to build a complete CMS from scratch.
    * Multi-Site capabilities - can have all my sites on one instance of Wordpress.
    * Can be controlled and developed with *composer*
* Why Backbone?
    * Wanted to leverage whatever tools Wordpress already have.
    * Was going to use it internally to for Wordpress admin.
### Process
* Basic project
    * Using Foundation for CSS and some JavaScript.
        * Not a designer. Basic components are okay. 
        * Huge fan of [Foundation Building Blocks](https://foundation.zurb.com/building-blocks/)
    * Added Vuejs for contact us form and captcha
        * Dry-run for adding registration micro-site.
    * Issues:
        * Webpack and gulp combination unwieldly
        * Need to learn how to use paninin (the static site builder) with webpack and without gulp client.
    * Trying to create admin interface in wordpress for managing entries.
        * Admin settings for captcha settings (public/private keys)
        * Be able to review entries and respond to them.
* Task
    * Had to learn how to create a wordpress plugin again
        * Plugin template generator [WORDPRESS PLUGIN BOILERPLATE GENERATOR](https://wppb.me/)
            * Used as the basis for my plugin
        * Added composer.json so I can enable php *autoload*
            * Point to autoload in site Vendor folder (outside of public) because I'm using composer to manage the complete site.
        * Trying to make it as object oriented as possible.
    * Was able to create custom endpoints.
        * [Postman](https://www.getpostman.com/) - to discover the wordpress API
        * [PHP Console Plugin]() - Chrome browser plugin to show php errors in chrome.
    
