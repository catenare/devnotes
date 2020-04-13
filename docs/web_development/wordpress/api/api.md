# Wordpress API
## Resources
* [REST API Handbook](https://developer.wordpress.org/rest-api/)

### Auth Plugins
* [JWT-Authentication](https://wordpress.org/plugins/jwt-authentication-for-wp-rest-api/)
* [Application Passwords](https://wordpress.org/plugins/application-passwords/)
* [OAuth 1.0a Server](https://wordpress.org/plugins/rest-api-oauth1/)
* [Basic Auth](https://github.com/WP-API/Basic-Auth)

### Using JWT-Auth
* Added to *composer.json*
    * Under require: `"wpackagist-plugin/jwt-authentication-for-wp-rest-api": "~1"`
* Added JWT constant to *wp-config.php* - `define('JWT_AUTH_SECRET_KEY','');`
* Access - local server - *http://paseo.demo/wp-json/jwt-auth/v1/token* Pass in username and password via form post.

## Notes
* pass **?_embed** as part of the url to get some content embedded. `http://paseo.demo/wp-json/wp/v2/posts?_embed`;
