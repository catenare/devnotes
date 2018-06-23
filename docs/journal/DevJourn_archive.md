# Journal
## 19 Nov. 2017
  * Focus on front-end
  * Added a placeholder partial for placeholder images using svg. Makes for a simple placeholder without being dependent on the network.
      * Does not work inside repeat sections.
  * Foundation xy grid is flexbox. Over 70% support in South Africa according to caniuse.
  * Settings.scss
      * $global-flex: true;
  * app.scss
      * @include foundation-xy-grid-classes;
  * Learning about flex with Foundation classes - Good youtube introduction.
  * Creating card layout using uswto.com blog page as template.
      * [ustwo blog page](https://ustwo.com/blog) - open sourced their web site. Using reactjs and wordpress.
  * Reactivated my codepen account.
  * Setup styleguide for site.
      * Initial layout
          * List of styles that we're using.
          * Goal is to be at least consistent.
          * Try to get an MVP going as quickly as possible.
  * Aiming to get the blog section going with work information at the bottom.
      * Resume in the footer with email list and contact me form.
    
## 20 Nov 2017
    * Trying to play with OBS - Open Source screen capturing software. Might be good for creating screen recordings. Will be text based rather than talking.

## 05 March 2018
  * Cleaning up my notes a little. Have many duplicates and some out of date. Plus, want to make sure current notes are included.
## 24 April 2018
  * Added API notes for PHP, Python and Node.js. Created section for **pipenv**.
## 25 April 2018
  * Jupyter Notebook notes added.

## 15 March 2018
* Using Vue and AWS amplfiy
  * Getting to know amp
    * Part of mobile hub
    * Similar to Google Firebase offering
      * Google Firebase is easier to use with their JavaScript SDK but is also more limited.
    * Features with amplify library
      * Auth
      * S3 storage
      * DynamoDB (Create DB on mobile hub but amplify needs aws javascript sdk to use)
      * Analytices (pinpoint)
      * Messaging (pinpoint) - Will use your SES domain if configured.
    * Other features
      * Hub - lightweight messaging service
      * Logger - logging service
      * Storage - local storage api
    * Get familiar with their API documentation
      * Very little documentation
      * Will need to read the API and look at the code to figure out how to use it.
  * Creating a basic app with Vue and amplify
    * Libraries
      * vuejs - vue-cli
      * vuex - vue-cli
      * vue-router - vue-cli
      * vee-validate
      * amplify
      * aws-sdk
      * mask
      * library for formatting phone numbers.
    * Create new project on mobile hub.
      * Get the project id from mobile hub
    * Need node and npm/yarn installed
    * npm install -g awsmobile vue-cli
    * Create vue project
      * `vue-cli `
    * Initialize awsmobile project
      * In vue directory - `awsmobile init {project id}`
    * Directory structure
      * src
        * components
          * Auth
            * Login
            * Signup
            * Verify
            * ForgotPassword
          * Auth.vue
          * Auth.html
          * Auth.scss
          * Auth.ts
        * App
        * lib
          * libraries you are accessing
        * Router
          * Welcome
          * Auth
          * Profile
        * Store
          * User
    * Functions
      * Signup user
        * Get additional attributes to save to cognito
        * Hash email to save as username
        * Manage errors
        * Save user information to Store
        * Form with showing password params in real-time
          * Using regex
      * Get verification code
        * Get username from Store
        * Resend if necessary
        * Go to login if successful
      * Login
        * Get user data from userinfo
        * Store data in Store
        * See if user is registered
        * Go to user registration page
        * Present forgot password
      * If user logs in and is registered
        * Go to profile page.
      * Profile
        * Profile view
        * Logout
        * Edit profile

