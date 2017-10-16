# Admin notes
## Admin and ajax
* [Using WP Async Requests](https://lkwdwrd.com/using-wp-ajax-async-requests/)
* [Ajax Async](https://lkwdwrd.com/ajax-async-wordpress/)

## Creating admin settings page
* Resources
    * [Creating wordpress settings page using wordpress rest api](https://torquemag.io/2017/06/creating-wordpress-settings-page-using-wordpress-rest-api/)
    * [Wordpress Theme Settings with settings api](https://www.sitepoint.com/create-a-wordpress-theme-settings-page-with-the-settings-api/)
* Options vs Settings
    * Setting is the newer of the two. More about building forms and managing setting
    * (Wordpress Codex Settings API)[https://developer.wordpress.org/plugins/settings/settings-api/]

* Authenticating with JWT Authentication for WP REST API for testing API with Postman
* [JWT Authentication for WP Rest Api](https://wordpress.org/plugins/jwt-authentication-for-wp-rest-api/) - needs to be installed and activated
1. Using Postman
    * post request
        * Url: http://paseo.demo/wp-json/jwt-auth/v1/token
        * Body Params
            * username
            * password
        * Response:
```json
{
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9qd3QuZGV2IiwiaWF0IjoxNDM4NTcxMDUwLCJuYmYiOjE0Mzg1NzEwNTAsImV4cCI6MTQzOTE3NTg1MCwiZGF0YSI6eyJ1c2VyIjp7ImlkIjoiMSJ9fX0.YNe6AyWW4B7ZwfFE5wJ0O6qQ8QFcYizimDmBy6hCH_8",
    "user_display_name": "admin",
    "user_email": "admin@localhost.dev",
    "user_nicename": "admin"
}
```
1. Sending a request
    * Create header
        * key: Authorization
        * Value: "token" value
    * Will authenticate when necessary.
### Enabling your plugin for wordpress
* Resources
    * *wp-api* - add as dependency for a script when you enqueue.
1. Setup
    * Create new folder *Settings* under *Admin*
    * Create new classes
        * Rest
            * Manages the Rest request and response
        * Settings
            * Manages the creation and management of the form, menu and database.
    * *Rest Class*
```php
<?php
/**
 * Created by IntelliJ IDEA.
 * User: themartins
 * Date: 2017/10/15
 * Time: 23:21
 */

namespace Paseo\Admin\Settings;


class Rest
{
    /**
     * @return bool
     */
    public static function permissions() {
        return current_user_can(Settings::$permissions);
    }

    /**
     * @return array
     */
    public static function get_settings() {
        return Settings::get_settings();
    }

    /**
     * @param \WP_REST_Request $request
     * @return \WP_REST_Response
     */
    public static function update_settings( \WP_REST_Request $request ) {
        $settings = array();
        foreach( Settings::$defaults as $setting => $value ){
            $result = $request->get_param($setting);
            if($result) {
                $settings[$setting] = $result;
            }
        }
        Settings::save_settings($settings);
        $updated_settings = self::get_settings();
        return rest_ensure_response( $updated_settings )->set_status(201);
    }

    /**
     * @param \WP_REST_Request $request
     * @return \WP_REST_Response
     */
    public static function check_settings(\WP_REST_Request $request ) {
        $settings = self::get_settings();
        return \rest_ensure_response($settings);
    }

}
```

## Authenticating with JWT Authentication for WP REST API
* [JWT Authentication for WP Rest Api](https://wordpress.org/plugins/jwt-authentication-for-wp-rest-api/)
1. Using Postman
    * post request
        * Url: http://paseo.demo/wp-json/jwt-auth/v1/token
        * Body Params
            * username
            * password
        * Response:
```json
{
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJodHRwOlwvXC9qd3QuZGV2IiwiaWF0IjoxNDM4NTcxMDUwLCJuYmYiOjE0Mzg1NzEwNTAsImV4cCI6MTQzOTE3NTg1MCwiZGF0YSI6eyJ1c2VyIjp7ImlkIjoiMSJ9fX0.YNe6AyWW4B7ZwfFE5wJ0O6qQ8QFcYizimDmBy6hCH_8",
    "user_display_name": "admin",
    "user_email": "admin@localhost.dev",
    "user_nicename": "admin"
}
```
1. Sending a request
    * Create header
        * key: Authorization
        * Value: "token" value
    * Will authenticate when necessary.


## Use timber as the templating engine
* composer require timber/timber
* Set location
    * user Timber\Timber; *Allow to use Timber*
    * Timber::$location = 'file path to template folder'; Ex: Timber::$location = '/Users/johan/wp/plugin/site/admin';
    * Timber::render('mytemplate.twig'); Ex: Will return false if not completed.

## Issues with using Rest API
* Limits access to customizing the site
    * Current tools for modifying templates won't work.
    * Front-end modification can be limited.
