# Headless CMS on Wordpress Multisite.
* Putting together a headless CMS network.
## Thinking
* Using Wordpress as the CMS component
* Adding other resources as necessary.
* Easier to deal with than Drupal.
* Commitment to API via current developments.
## Sites
* Paseo Baptist Church
* Paseo Center - Daycare and Preschool
* The Martin Family
* Personal Site
	* Currently hosted at Github
## Wordpress Development
### Wordpress API Form plugin - front-end and admin
* folder layout
	* **site** - public assets for plugin
	* **src** - PHP Classes for the plugin
		* **site** - alias to outside **site* folder
		* **Main.php** - main entry class for plugin
		* **Admin** - Admin classes for plugin
		* **Rest** - Rest endpoints for plugin
	* **paseo-wp-form-api.php** - entry script for plugin
	* **build** - folder for building javascript/css (front-end) of admin plugin
		* Includes *node_modules*
			* Using *webpack* to build the assets.
		* **src** - CSS/JS assets for plugin
		* Build script will push assets to **site/assets**
#### Creating admin screen for setting options and to view entries in contact us form.
* Using REST API
* Will use REACT as the engine
* Updates/changes managed by REST
##### To Do
- [ ] Add javaScript to admin site
- [ ] REST end-point for admin settings
- [ ] Modify theme plugin to put all front-end build info into *build* folder.