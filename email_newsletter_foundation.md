# Email formatting using Foundation from Zurb
## [Foundation](http://foundation.zurb.com/emails.html)

## Notes
* [Github Repository](https://github.com/catenare/newsletter-builder)
* Setup
  * 2 main branches in this Repository
  * __master__ - tracks the the foundation email template - [Zurb email template](https://github.com/zurb/foundation-emails-template)
  * __default__ - base repository from which we create our newsletter
* Instructions
  1. Checkout __default__ branch. ```git checkout default```
  1. Create branch for newsletter from __default__ branch. ```git checkout -b feb2017```
  1. Content for newsletter is in ```src/pages/index.html```
  1. Layout is ```src/layouts/main.html```
* Running the server
  1. ```npm install``` - install all the modules
  1. ```npm start``` - start the server and open the browser
  1. ```npm run zip``` - build the zip files. Zip file was in ```dist/index.zip```
