# Developer Journal
My Developer Notebook is at [Developer Notebook](http://www.catenare.com/devnotes/)
Brain dump of notes I'm making while working on projects. Can use these to update my developer notebook.
***
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