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
***
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

***
## Wednesday, 13 June 2018
* Google Chrome is a random error, slow nightmare on Mac OS X but it also seems to have the better development tools available. Especially for Vue and Angular development. Don't really have time to keep switching development environments but will need to check out Firefox.
* Ran into issues with Visual Studio Code on Mac OS X. Using the built-in terminal caused my computer to become unresponsive when I had multiple terminals open. Deleted the application and then downloaded it again. All the settings and plugins were still there and seems to be working better. I'm also not using the built-in terminal anymore.
* Even in TypeScript. Composition over inheritance and program to an interface.
* Flyway migrations I'm always using - sql commands:
	* `ALTER TABLE IF EXISTS RENAME COLUMN column_name TO new_column_name`
* SQLAlchemy - create one to one relationship between Users and Roles. Allows me to get User.role.title. [One-to-One Relationship](http://docs.sqlalchemy.org/en/latest/orm/basic_relationships.html#one-to-one)
```python
class Users(base):
    __table__ = Table(c.TABLE_USER, meta, autoload=True, autoload_with=engine, extend_existing=True)
    role = relationship("Roles", uselist=False, back_populates="user")


class Roles(base):
    __table__ = Table(c.TABLE_ROLE, meta, autoload=True, autoload_with=engine, extend_existing=True)
    user = relationship("Users", back_populates="role")
```
* Setup AWS Cloudfront to redirect to index.html for html5 history mode.
	* Edit *Error Pages* in cloudfront. Redirect errors to index.html
	![](/images/lookfindme_aws/cloudfront_config_error_response.png)
	* Create custom error response
	![](/images/lookfindme_aws/cloudfront_config_html5_routing.png)
	* Redirect http to https - Only shows when ACM certificate is created.
	![](/images/lookfindme_aws/redirect_http_to_https.png)
* Issue with vue. Only seems to be with some modules. Trying to figure out what. Changed from index.vue, to name.vue. Doesn't seem to work.
```
ERROR in /Users/themartins/Documents/Projects/johan/projects/clients/Eren/LookFindMe/lookfindmeadmin2/src/router.ts
10:24 File '/Users/themartins/Documents/Projects/johan/projects/clients/Eren/LookFindMe/lookfindmeadmin2/src/components/Industries/Industries.vue' is not a module.
     8 | import Help from "@/components/Help.vue";
     9 | import Settings from "@/components/Main/Settings/Settings.vue";
  > 10 | import Industries from "@/components/Industries/Industries.vue";
```
### AWS API Gateway
* Goals
	* API endpoints
		* admin - authenticated administration access. 
		* user - authenticated user access
		* site - basic site access for front page items.
			* limit to get only.
		* test - post number and get double back. Basic test
	* Routes same in Flask app.
	* Configured this way in nginx proxy.
	* Use *cognito* user to authenticate to API Gateway.
	* Backend access on VPC network. No public access to API unless via api gateway.
* Resources
	* Urls
		* [Admin Server](adminapi.lookfindme.com)
		* [API gateway](api.lookfindme.com)
		* [Admin Site](admin.lookfindme.com)
* Issues
	* Seems like you can only do a VPC with a load balancer. Don't really want to do that since that is an additional cost.
	* Might have to only do http request. Might be able to limit access to only the API gateway.
* Setup EC2 Server on AWS with LetsEncrypt certificate.
	* Create LetsEncrypt certificate for EC2 server.
		* `ssh -i lookfindmeecs.pem ubuntu@adminapi.lookfindme.com`
		* Need to open port 443 to public access to configure certificate. ![](/images/lookfindme_aws/security_group_access.png)
		* [Certbot Ubuntu 16.04 with Nginx](https://certbot.eff.org/lets-encrypt/ubuntuxenial-nginx)
		* Instructions worked flawlessly. Includes automatically setting https redirect.
	* Updated my *nginx* config.
	* Change to socket
```
upstream flask {
		server unix:/tmp/lookfindme.sock
}
```
* `sudo nginx -t` - validate configuration
* cd into *lookfindmeapi*
	* `uwsgi --ini uwsgi.ini --plugin python3` - starts uwsgi server.
	* `uwsgi --stop /tmp/lookfindme.pid` - stops uwsgi server
* Tested with Postman - can get positions and double test works. Server is now live.
* Configure *vue.config.js* proxy. Want to proxy all requests to  live site to local site while working on code. [Vue Cli](https://cli.vuejs.org/config/#devserver-proxy)
```js
  devServer: {
    proxy: {
      "https://adminapi.lookfindme.com": {
        target: "http://localhost:5000"
      }
    }
  },
```
#### Connect server to API
* Settings
	* EC2 
		* Private IP: 172.31.88.130
		* VPC: vpc-2e090456
		* Subnet: subnet-6790f148
			* Private DNS: ip-172-31-88-130.ec2.internal
#### Setup API Gateway with https access.
* Adding a custom domain name: ![](/images/lookfindme_aws/create_aws_api_domain_name.png)
* In GoDaddy, point api.lookfindme.com to api url - d107qy4n4o7sd9.cloudfront.net: ![](/images/lookfindme_aws/dns_cname_config.png)
* Create http proxy - admin: ![](/images/lookfindme_aws/api_http_proxy.png)
* Deploying an API
	* Under Actions, select Deploy API - ![](/images/lookfindme_aws/api_deployment_overview.png)
	* Choose a deployment or create a new deployment - ![](/images/lookfindme_aws/api_deployment_2.png)
	* Enter deployment name and other info - ![](/images/lookfindme_aws/api_deployment_3.png)
	* Deployment Overview and URL for external access - ![](/images/lookfindme_aws/api_deployment_4.png)
* Setting up the custom domain name to point to the staged API
	* Left path empty
	* Stage points to Staged API ![](/images/lookfindme_aws/api_deployment_custom_domain.png)
	* API Test: ![](/images/lookfindme_aws/api_deployment_postman_test.png)
* Setting up a client certificate - see if we can get it to work. [Client Side SSL Not Working - StackOverflow](https://stackoverflow.com/questions/34175361/client-side-ssl-not-working-with-aws-api-gateway)
	* Seems like nginx is looking for certificates in specific locations - /etc/ssl/newcerts
	* */etc/nginx/awsapigateway.crt* - Created cert file in nginx config folder. - **Verify the whole certificate was copied over.** ![](/images/lookfindme_aws/api_deployment_client_certificate.png)
```
    listen [::]:443 ssl ipv6only=on; # managed by Certbot
    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/adminapi.lookfindme.com/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/adminapi.lookfindme.com/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot
    ssl_verify_client on;
    ssl_client_certificate awsapigateway.crt;
```
Seems like we have a working system.

* Pushing frontend to admin.lookfindme.com - `awsmobile publish`. This publishes and pushes the site to cloudfront.
### General Notes
* Current *lookfindmeapi* deploy to ec2 setup
	* `git pull origin master`
	* `cd tools/database`
	* `gradle migrate` - any changes need to be applied to the database
	* `cd ../../` - back in *lookfindme* directory.
		* `uwsgi --stop /tmp/lookfindme.pid` - stops uwsgi server
		* `uwsgi --ini uwsgi.ini --plugin python3` - starts uwsgi server.
	* Working on lookfindme.
		* Setting up environment variables. vue-cli supports .env files. - [Mode and Env](https://cli.vuejs.org/guide/mode-and-env.html#example-staging-mode). Need to differentiate between local api server and ec2 api server.
		* `const ProductionUrl = (process.env.VUE_APP_API_URL) ? process.env.VUE_APP_API_URL : "";` - Only include url in Production build. Local version has proxy to local api server.
		* Resolve issue with *vue' is not a module* - did it before but didn't take notes. [typescript building error when import .vue file with separate .ts file](https://github.com/vuejs/vue-cli/issues/1104). 
```ts
// @ts-ignore  
import HelloWorld from '@/components/HelloWorld/HelloWorld.vue'; 
```
Makes the error go away.
#### Still having issues with CORS on API Gateway.
Want to configure it to allow from any *.lookfindme.com domain. But there seems to be an issue with creating new resources. It just spins. Might have to close my browser and reopen. On the plus side, computer is working much better today. Seems that using terminals in Visual Studio Code is just asking for trouble.
Error: "'Access-Control-Allow-Origin: *'". Seems to be a combination of Chrome browser and server. Trying to enable CORS on the API gateway and see if that helps.
* Resolved:
	* Added header to *nginx* config.
```conf
        location /admin {
                add_header 'Access-Control-Allow-Origin' '*';
                include /etc/nginx/uwsgi_params;
                uwsgi_pass flask;
                uwsgi_param Host $host;
                uwsgi_param X-Real-IP $remote_addr;
                uwsgi_param X-Forwarded-For $proxy_add_x_forwarded_for;
                uwsgi_param X-Forwarded-Proto $http_x_forwarded_proto;
}
```
Going to try and add it to the server level.

***Below does not work***
```conf
add_header 'Access-Control-Allow-Origin' '*';

        location / {
                # First attempt to serve request as file, then
                # as directory, then fall back to displaying a 404.
                try_files $uri $uri/ =404;
        }
```

* Restart nginx on Ubuntu - `sudo systemctl restart nginx.service`

***To get this work. Have to configure nginx with *add_header* to allow 'Access-Control-Allow-Origin' to work.*** Configuring the API gateway doesn't matter.
* https://vpc-lookfindme-oxhmtdgaa63hkgxaxtmivoqkhm.us-east-1.es.amazonaws.com/ - Elastic Search URL
### Add Ability to create and edit membership to admin site.
* Have membership_level enum - *membership_level*
* Adding foreign_key constraint. Want roles to come from role table. Creating Flyway Migration using sql below. Seems that it is easier to drop a column rather than trying to change it to UUID.
```sql
ALTER TABLE IF EXISTS public.memberships
	DROP COLUMN member_role;
ALTER TABLE IF EXISTS public.memberships
	ADD COLUMN role_uuid UUID REFERENCES role (uuid);
ALTER TABLE IF EXISTS public.memberships
	RENAME TO membership;
```
~~Just being anal about renaming *member_level* to level.~~

* Current time: 00:10
* Creating a test for my membership service.
	* Add new membership
	* Find a new membership
	* Update a current membership
	* Can't delete a membership because it may not be available but a user might still be on it.
* Had to fix and issue with migrations. Can't use *level* as a field name. Changed the migration. 
	* - Fix flyway - `gradle flywayRepair` - fix issues with migration.
* Working with raw json in python - [Pyton Json](https://realpython.com/python-json/)
```python
json_string = """
{
    "researcher": {
        "name": "Ford Prefect",
        "species": "Betelgeusian",
        "relatives": [
            {
                "name": "Zaphod Beeblebrox",
                "species": "Betelgeusian"
            }
        ]
    }
}
"""
```
* Apparently Flask does deserialise the json data when you use request.get_json()
* Completed adding memberships to code. Added Schemas and code to add, retrieve memberships. Need to add code to update memberships. Don't think we have code to update records.
* Completed adding the filters too. Testing as you go along makes it easier to insure everything is working. Plus, helps with content switching.
***
## Thursday 14 June 2018
Spent all morning updating the work machine. It downloaded the latest updates. Removed Chrome from my startup items. Don't know how it got there. Also removed some cruft left over from a Samsung install. Concerned that my iPad is about to die. Really like using YouTube for playing music from the iMac. Also, seems that the issue with Visual Studio Code was trying to use terminal in it.

* Today's Goal 
	* lookfindme
		* Publish admin site and connect to demo site.
			- [x] Able to update membership and it shows on demo site.
			* Add about and it shows on demo site.
			* Terms and Privacy updated on demo site.
			* Change industry titles and it shows on demo site.
			* Change front and industry image.
		* Why is_enabled, is_test and is_published?
			* is_enabled = shows up on the public site
			* is_test = does not show up on the public site. Used when running tests. Want to be able to run tests on live site.
			* is_published = once it has been made available to the general public, it cannot be deleted anymore. *is_published* and *is_enabled* has to be both activated for it to show on the public site.
		* Tasks
			1. [x] Add is_test column to all tables. Can then checked if record was generated by tests.
			* Memberships
				- [x] Update memberships - send post request to membership/id
				- [x] is_published flag. Once published, cannot be deleted.
			* Industries
				- [x] Add new industry
				- [x] Update title and image of current industry
				- [x] Can disable but not delete.
					- [x] Add is enabled flagged
					- [x] Add is_published flagged.
		* Connect cognito to AWS API Gateway
			* Able to use AWS library when posting to API vs using local library when working locally.
	- [x] Update marshmallow on local machine.
	* ~~Spend an hour working on trying to connect spring to a database and making an API call with it.~~ ***Not going to happen today***
* Commands in Term2 shell that I should memorise since I use them all the time.![](/images/desktop/screen_desktop.png)
	* **Command D** - split horizontally
	* **Shift Command D** - split vertically
* Upgrading stuff. We will see how this goes.
	* sdk - upgrade java related tools.
	* nvm - upgrade node to 10.4.1 and reinstall packages
	* lookfindme - upgraded packages. Still can't upgrade rxjs and @types/node because of issues with vue. Have to stick to rxjs@6.2.0 and @types/node@10.2.1
	* Updated IntelliJ from drop-down tool.
	* Trying to upgrade my marshmallow package. First removing marshmallow-sqlalchemy. Didn't use it. Seems that pipenv requires me to remove marshmallow first and then reinstall it. Also removing some other packages. `pipenv uninstall jsonschema psycopg2 gunicorn blinker marshmallow`
	* Had to create an update service in my services class because it didn't have one before. 
	* Keep getting errors about psycopg2 requiring the binary driver. Uninstalled the psycopg2 module and just left the psycopg2-binary module. Now not being found by the database server string. Reinstalled psycopg2 and that seems to work. Will have to figure out why the psycopg2-binary isn't working but not going to deal with it right now.
	* Seems to have some issues around marshmallow update.
		* Updated marshmallow does not require the .data attribute when I serialise to json. Had to remove that.
	* Updating data
		* Current config returns the total number of records processed rather than the updated record. Want to returning feature of the call.
			* Note to self. See if you can find the tests for a module to find out how to use the module.
			* Will have to investigate further later. Taking too much time just trying to get it to work. [Commit with test data related to *update_args*](https://github.com/zzzeek/sqlalchemy/commit/c90f0a49f332867f6b337c79ddf192299788667f)
* Going to try and get rid of psycopg2 error that is bugging me. Uninstalling the psycopg2 package. Going to install `pipenv install --no-binary :all: psycopg2` We will see how well it works. [Fix Psycopg2 Warning](https://gist.github.com/turing4ever/883ec1b0f92274714b867ffacee85285)
```
export PIP_NO_BINARY=psycopg2
pipenv install psycopg2
```
* ***Error message is gone now.***
* Create industries setup and tests.
	* Add new industry
	* Update an industry
	* Get one industry
	* Get list of industries
	* Test created and now testing the test.
	* **Tests pass. Now moving on to the front-end.** 
* AWS Amplify and API Gateway.
	* Get API Gateway settings
* REST vs PUT - PUT is suppose to be idempotent so probably better for updates. [Restful API Tutorial](https://restfulapi.net/rest-put-vs-post/)

* Testing the API Gateway with an Auth Token.
	* Setting up authorisation for API Gateway
		* User Pool is already setup via Mobile Hub.
			1. Open API Gateway Console.
				1. Select Authorizers 
				1. Create new Authorizer
					1. Select Cognitor as the provider
					1. Select the UserPool from the list when you click in the field box.
					1. Token Source is *Authorization* ![](/images/lookfindme_aws/create_auth.png)
				1. Save.
			1. Test your provider
				1. I'm already using aws amplify for site authentication
				1. Grabbed the *JWT* token from the JavaScript Console
				1. Copy and paste only the token (no quotes) into the test  box. ![](/images/lookfindme_aws/test_credential.png)
				1. Click test and see if your authorisation works.
			1. Deploy to your API
				1. First add authorization to your resource. ![](/images/lookfindme_aws/resource_auth.png)![](/images/lookfindme_aws/resource_auth_detail.png)
				1. Deploy your API
			1. Can test with Postman by providing JWT token.
* Using *ngrok* to try and use it to access API Gateway
	* Issue with invalid header. Solution: [Invalid Host Header when ngrok tries to connect to React dev server](https://stackoverflow.com/questions/45425721/invalid-host-header-when-ngrok-tries-to-connect-to-react-dev-server?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa)
		`ngrok http 8080 -host-header="localhost:8080"`
		`ngrok http --host-header=rewrite 8080`
	* Getting ngrok going `ngrok http 8080 -host-header="localhost:8080"`
* Back to working on front-end
	* Get industries from backend
		* Create model of industry
		* Backend service to get industries
				* Refactor to create one get request.
	* Getting Roles and enums too. For downloads. Have tests working on server. Now working on front-end side. Still not done.
	* Adding new add forms.
## Friday 15 June 2018
Seems like a lot of time working on getting the backend services to work. Machine was updated and updated local software. Going to resist the desire to update the software again today. I actually need to try and get some stuff done. Did kinda figure out how setup an AWS API Gateway with authentication and how to test it. Definitely need to write up these notes as blog posts.

Need to take Hennely's talk to heart about estimating. I'm way off when it comes to estimating the time it will take. Have to post sites today.

Also want to create an RSS feed for my blog. RSS feed is already available on the Wordpress site. Just need to figure out how to forward RSS requests at https://www.johan-martin.com/rss to https://api.paseo.org.za/johan/rss. If using Apache, I would jus t proxy it. Don't know if we can do that with Google Firebase. Might have to create a custom function. [URL Redirects](https://firebase.google.com/docs/hosting/url-redirects-rewrites) - Might have to use that in the short-term. Will look later.

* Updated Goals 
	* lookfindme
		* Publish admin site and connect to demo site.
			- [-] Able to update membership and it shows on demo site.
			- [ ] Add about and it shows on demo site.
			- [ ] Terms and Privacy updated on demo site.
			- [ ] Change industry titles and it shows on demo site.
			- [ ] Change front and industry image.
* Rolling out admin site today.
	* Setting up AWS access
		- [ ] API Gateway
			- [ ] Create new cloudfront endpoint in Godaddy
			- [ ] Import certificate into API Gateway
			- [ ] Create certificate to add to backend server
			- [ ] Setup authorization with Cognito
		- [ ] Cognito
			- [ ] Use email as the authentication option
			- [ ] Create app to allow user pool authentication
			- [ ] Email notification for setting up a new user
		- [ ] DynamoDB
			- [ ] Create Settings object with all settings that we push into DynamoDB

Created a basic blog post with everything I need to do to get the API up and running. Part 1 of a series.

Working on the membership form. Get a list of memberships. Popup window to view and edit it.

* Vuetify notes
	* v-container - page level
	* v-layout - section or component level
	* v-flex - specific item. sets flex on this level.
		* inside component should just us v-flex

- [] Create membership list item component. Going to show it as a v-card. Need to look at content for membership in google site.
		* Have to include `// @ts-ignore` in front of all import statements to keep vue from freaking out.
		* Created the ListItem. Now need to get it to show the Item correctly. Will do that when I come back from my run.
		* Removed separate List component. Just creating a separate ListItem to format individual list items.
		* Creating a new membershipModel that includes a meta object. Object contains uuid and the action taken. Idea is that when an action happens in the listItem, I can update the membershipModel and get those results. We will see if that works. Don't think it's going to work because I'm no longer doing a separate list component. Now, List is actually the main component and all actions should just bubble up to the Membership component. Actions will be. Edit, Enable, and delete if not published.
		* Adding additional parameters to the membership. jobseekers - how many you can interact with and industries is how many you can search across.
		* Basic card created. Also realize that one cannot edit a membership that has already been published. Would cause too much confusion. So, once it is created and published, it can no longer be edited.
		* Trying to get form out of dialog that is holding a form. 

## Random notes.
Hate it when I lost a thought that I just had and wanted to write down. Really annoying!!!!

* Going to run at 13:57.
* Got back at 15:19
* Creating a *prettier* - `.prettierrc` configuration file. Hope I can get it to work with Vue files.
* Pre-commit hooks for node/npm
	* [Husky](https://github.com/typicode/husky) - can configure package.json file with precommit hooks.
	* [Pre-commit hooks](https://pre-commit.com) - manage and maintain precommit hooks.
* Installed `npm install eslint-plugin-prettier eslint-config-prettier --save-dev`
* Configuration:
	* `editor.formatOnSave`
* [Prettier VSCode Plugin](https://github.com/prettier/prettier-vscode)
* Typescript array - string[] or Array<string>
* Associate template.html files as vue-html files for syntax highlighting to work again.
* Computer is running really slow. Have to restart to see if it gets any better.
* Don't know why it's going so slow.
* After quitting out of Visual Studio Code, everything seems better. Only change I've made was to the prettier config. Haven't changed anything else. Also, did change html config to jsbeauty or something similar. Might be related to that. But does seem that visual studio code gets bogged down sometimes.
* My version node seems to keep crashing with Vue. Downgraded to  10.1.0 that I had before. Will see if it still crashes as much. `echo "10.1.0" > .nvmrc` in my current project folder. `nvm alias default v10.1.0` to get back to previous version. Going to attempt to upgrade my copy of nvm to latest tagged version. Getting really frustrated with constantly having to go back to the documentation. Ok. Had to restart IA writer. Seems to be working better now. Don't know why this machine randomly starts slowing down.
* `<component :component="passedin" />` - Figure out which value is which.
* Well, seems that it is still crashing even though I've downgraded my NPM. Restarting and upgrading. See if that makes any difference. Think my setup might just be bad news.
* Restarting everything and see what works.
* Reinstall rxjs@6.2.0 and @types/node@10.1.2.
	* Just uninstalling rxjs wasn't enough. Still getting errors. Won't be able to build the project with those errors.
* Getting stuck on formatting the site. Really need to up my CSS skills. It takes me way too much time to format anything.
* Still trying to at least style the form to look like someting interesting.
* Finally working on the form. Got the basics done. Now trying to figure out how to take an array and make it into an editable area while allowing for additional items to be added.
* Reduced the number of items being pulled into my form. Seems to have eliminated some of the issues with my node crashing.

## Saturday 16 June 2018
* lookfindme
		* Publish admin site and connect to demo site.
			- [-] Able to update membership and it shows on demo site.
			- [ ] Add about and it shows on demo site.
			- [ ] Terms and Privacy updated on demo site.
			- [ ] Change industry titles and it shows on demo site.
			- [ ] Change front and industry image.
* Rolling out admin site today.
	* Setting up AWS access
		- [ ] API Gateway
			- [ ] Create new cloudfront endpoint in Godaddy
			- [ ] Import certificate into API Gateway
			- [ ] Create certificate to add to backend server
			- [ ] Setup authorization with Cognito
		- [ ] Cognito
			- [ ] Use email as the authentication option
			- [ ] Create app to allow user pool authentication
			- [ ] Email notification for setting up a new user
		- [ ] DynamoDB
			- [ ] Create Settings object with all settings that we push into DynamoDB
Formatting front-end takes forever. Every framework has its own idiosyncrasies plus now everything is flex box. Form is taking forever too.
 
* Membership form status
	- [ ] - Form in own component
	- [ ] - In dialog box
	- [ ] - model tied to form
	- [ ] - Able to change data
	- [ ] - Array to add new benefit items.
* Huge fan of prettier. On save is too resource intensive. Works fine to just do it when saving the data.
* Going to attempt to enable eslint feature.
* Making the detail item into its own component. Anything that takes more than a couple lines of code needs to be its own component.
* Trying to get a filter to work. Idea is that we will format the number as a regular number but it is actually stored as a integer. 
* Also realising, because the v-module is reactive, we need to make a copy of it and update the copy. Else, we update our actual data and it is an issue when you hit the reset butt.
* Working on the filter now.
	* Vue does have a filter option.
	* Trying to figure out how to use the filter option in a vue component class.
* Handling form submission in Vue
	* `<form @submit.prevent="handleSubmit"></form>`
	* `handleSubmit() {}`
* Using functional components for very basic presentation. [Vue Functional Components](https://alligator.io/vuejs/functional-components/) - [Render functional components](https://alligator.io/vuejs/render-functional-components/)
* Using filters with vue component class
```ts
@Component({
  filters: { trim() { /* some code here */ } }
})
class YourComponent extends Vue {
}
```
* Have a form that I need to use to update local information. Form gets its values passed to it when I click on the edit button. Want to leave the original values alone and only mess with the copied values.
	* Watch the imported property
	* Assign the oldval of the property to the form model. This means the model now points to the local variable.
	* Update the data and submit that data.
	* Problem now is to deep copy/clone the object so everything is disconnected. Might have to install lodash.
	* Tried with an observable. Still getting the full copy. Need to figure out how to clone an object in JavaScript.
* Clone a JavaScript object. Just wants to make sure that the original is not impacted by any changes I make.
```js
JSON.parse(JSON.stringify( obj ));
```
* Although the above method works, it feels like a hack. Decided to install lodash and use it's cloneDeep method [CloneDeep](https://lodash.com/docs/4.17.10#cloneDeep).
* Now have to save the data back to the database. Show the price divided by 100. Do it when we clone the record.
* Using loads to pick only the values I want to save. Complete record is not necessary. *this.membership* is the object with the updated data. Unfortunately, it also has all the data retrieved from the server including created and updated fields that are not required here. Local model is the *new Membership()*. Grab the keys from it and use that to only grab the properties I need for saving into the database. 
* Huge fan of lodash.
```ts
    const formData = _.pick(this.membership, _.keys(new Membership()));
```
* Huge fan of using models to manage my objects. Have to only update the model and everything else is updated everywhere else. Big time saver for getting work done. Had to add and remove properties from an object. Because I have a model for it, it's as simple as editing the model.
* Just created a blog post for my blog about lodash. Going to setup medium next week.
* Just started using the AWS Amplify Logger utility again. Great way to implement logging and not have it show up on the live site. `const logger = new Logger('name');`. Actually using it.  `logger.debug('what I need to log');`. [Logger Guide)](https://aws.github.io/aws-amplify/media/logger_guide)
* Trying to save data to the server. Need to remove the uuid key. Seems like the update is failing if the uuid key is one of the fields included. Of course, working on a slow machine. Really need to get this done so I can apply for real work. This is killing me but I promised. 
* Ok. Got the delete with permission to work. Getting the enabled setup now. Going to try and finish the industries too. Only requirement there is that you can add a new industry and edit maybe the image. Everything else stays static.
* Got enable and disable to work. Need to put logic for is_published on server side rather than just on the client side.