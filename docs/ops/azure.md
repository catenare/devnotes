# Azure Notes

# Using Active Directory for remote login
## Register a new web application
1. Select *Azure Active Directory*
1. Choose *App registrations*
1. Click on *New Application registration* - current layout close to top toolbar.
1. Enter the name
1. Application type - *web app/API*
1. Sign-on Url
    * End-point that will process and determine if the user is logged in.
    * *http://{wordpress-site}/wp-login.php* is the endpoint for wordpress
### Creating keys for API access
1. Select *Azure Active Directory*
1. Click on *App registrations*
1. Click on your app
1. Click on *All Settings* - current layout - bottom right corner.
1. Click on *Keys* under *Api Access*
1. Under keys
    * Enter a description
    * Choose duration
    * Click *save* icon
    * Copy secret key. Will go away when navigating away from this page.
1. Settings
    * **Application ID** - *Can also be referred to as the Client ID. Refers to your application so Azure can tell where to authenticate.*
    * **API Key** - *Generate under All Settings -> Api Key*
### Determine Tenant ID
* Tenant Id is the the id of the Azure Directory you are using.
1. Click on *Azure Active Directory* - far right column under main list of services
1. Click on *Properties*
1. *Directory ID* is the same equivalent of *Tenant ID* when referring to this Active Directory.
