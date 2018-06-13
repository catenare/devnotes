# Developer Journal
My Developer Notebook is at [Developer Notebook](http://www.catenare.com/devnotes/)
Brain dump of notes I'm making while working on projects. Can use these to update my developer notebook.
## Monday, 11 June 2018
### Vuejs with vue-cli
* [Example Project - lookfindme Admin](https://github.com/catenare/lookfindmeadmin2)
* Proxy config - *vue.config.js*
	* Can add webpack configuration using *ConfigureWebpack* 
### LookFindMeAdmin site
* Using Vuejs with vue-cli 3
* Monday 11 June 2018 @ 15:23
	* Got rxjs ajax to work with VueJs.
		* `import {ajax} from "rxjs/ajax";`
	* Admin command line client
		* `pipenv install -e .` - installs the command line client locally.
		* `lookfindme` - list of commands available.
		* `lookfindme insert_site` - read info from json document (app_data.json, industries.json) and populate database table(s).
		* Settings table has multiple json objects to store setting data. Don't expect to do any reporting on those fields. Mostly text and will be accessed only at build/create time.
		* Settings table saves all changes. Access to the latest settings if via the site_uuid and latest version based on updated_at column.
	* All components are under the *settings.vue* component
		* Need to figure out how to get the updated information back from the components.
		* Show everything as fields.
		* Update the database after the fields have been updated.
	* Add form array in VueJS -[v-model-array-multiple-input](https://stackoverflow.com/questions/34825065/vuejs-v-model-array-in-multiple-input)
```ts
new Vue({
  el: '#app',
  data: {
    finds: []
  },
  methods: {
    addFind: function () {
      this.finds.push({ value: '' });
    }
  }
});
```
```html
<div id="app">
  <h1>Finds</h1>
  <div v-for="find in finds">
    <input v-model="find.value">
  </div>
  <button @click="addFind">
    New Find
  </button>
</div>
```
* [Vue Quill Editor](https://surmon-china.github.io/vue-quill-editor/) - vue-quill-editor - able to set options via *:options* directive.
* Python Notes - my PHP days keep haunting me.
list comprehension: list = []
## Tuesday, 12 June 2018
* Inserting data into jsonb via Python. Let python do it's thing. Seems like SQLAlchemy automatically serializes it's data into jsonb format.
* Getting ajax to work with rxjs ajax - options [Ajax Request](https://stackoverflow.com/questions/41286476/rxjs-5-simple-ajax-request)
```ts
interface AjaxRequest {
  url?: string; // URL of the request
  body?: any;  // The body of the request
  user?: string; 
  async?: boolean; // Whether the request is async
  method?: string; // Method of the request, such as GET, POST, PUT, PATCH, DELETE
  headers?: Object; // Optional headers
  timeout?: number;
  password?: string;
  hasContent?: boolean;
  crossDomain?: boolean; //true if a cross domain request, else false
  withCredentials?: boolean;
  createXHR?: () => XMLHttpRequest; //a function to override if you need to use an alternate XMLHttpRequest implementation
  progressSubscriber?: Subscriber<any>;
  responseType?: string;
}
```
* Format json for testing with postman - [Free Json Formatter](https://www.freeformatter.com/json-formatter.html#ad-output)
### AWS Amplify
* Create new password when creating user in the admin console.  *auth_user* is the CognitoUser object returned when initially logging in. Method is *Auth.completeNewPassword*. Have to use it when creating user manually. *from* is rxjs observable.
```ts
export const UserSignIn$ = (username, password) => {
  return from(Auth.signIn(username, password));
};

export const CreateNewPassword$ = (user: IUser) => {
  return from(
    Auth.completeNewPassword(user.auth_user, user.new_password, user.auth_user.challengeParam
      .requiredAttributes)
  );
};
```
## Wednesday, 13 June 2018
* Google Chrome is a random error, slow nightmare on Mac OS X but it also seems to have the better development tools available. Especially for Vue and Angular development. Don't really have time to keep switching development environments but will need to check out Firefox.
* Ran into issues with Visual Studio Code on Mac OS X. Using the built-in terminal caused my computer to become unresponsive when I had multiple terminals open. Deleted the application and then downloaded it again. All the settings and plugins were still there and seems to be working better. I'm also not using the built-in terminal anymore.
* Even in TypeScript. Composition over inheritance and program to an interface.
* Flyway migrations I'm always using - sql commands:
	* `ALTER TABLE IF EXISTS RENAME COLUMN column_name TO new_column_name`
* Setup AWS Cloudfront to redirect to index.html for html5 history mode.
	* Edit *Error Pages* tase in cloudfront. Redirect errors to index.html
		* ![](/images/cloudfront_config_error_response.png)
	* Create custom error response
		* ![](/images/cloudfront_config_html5_routing.png)
### AWS API Gateway
* Goals
	* API endpoints
			* admin - authenticated administration access. 
			* user - authenticated user access
			* site - basic site access for front page items.
				* limit to get only.
		* Routes are setup this way in python app.
		* Configured this way in nginx proxy.
	* Use *cognito* user to authenticate to API Gateway.
	* Backend access on VPC network. No public access to API unless via api gateway.