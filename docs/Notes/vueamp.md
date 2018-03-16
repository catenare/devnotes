# Notes
## 15 March 2018
### Using Vue and AWS amplfiy
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

