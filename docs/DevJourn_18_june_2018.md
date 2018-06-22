# Developer Journal Week of 18 June 2018
Goal this week is to at least finish the admin part of *lookfindme*. So close but for the details.

## Monday, 18 June 2018
Still working on lookfindme admin site. Having issues with the industries list. Not updating if there is only one item in the json array. Don't know why that it is. It will save okay but it seems to have an issue updating. Will check the interwebs else might just convert it to an array or a string with pipe characters and store it as a string. The data is actually being sent. The issue is the it is not being saved.
* Using integers for all my money. Listened to a webcast about using integers for currency rather than floats. Requires a little more on the front-end side but then, I'm trying to avoid anything on the front-end that will have to be redone on the backend anyway. 

### lookfindme
* Look into why the industries list of positions doesn't want to update if there is only 1 item in the list.
	* Resolved by adding *synchronize_session='evaluate'* - `            result = self.query.filter(self._table.uuid == uuid).update(update_values, synchronize_session='evaluate')` [Query Details](http://docs.sqlalchemy.org/en/latest/orm/query.html?highlight=query)
* Now have to work on the enable/disable issues.
	* Fix the issue with the database not respecting UUIDs passed in from the API. Only seems to be an issue when I'm not passing it in as a primary key. No problem if it is a primary key. [SQLAlchemy Schema Table](http://docs.sqlalchemy.org/en/latest/core/metadata.html#sqlalchemy.schema.Table) - [Postgresql.UUID](http://docs.sqlalchemy.org/en/latest/dialects/postgresql.html?highlight=uuid#sqlalchemy.dialects.postgresql.UUID)

**database/engine.py**

```python
class SiteSettings(base):
    __table__ = Table(
        c.TABLE_SITE,
        meta,
        Column('site_uuid', postgresql.UUID(as_uuid=True)),
        autoload=True,
        autoload_with=engine,
        extend_existing=True
    )
```

**routes/admin.py**

```python
@bp.route('/site/<uuid:site_id>', methods=['GET'])
def site_get(site_id):
    try:
        result = SiteServiceModel.get_json_data(site_id)
    except SQLAlchemyError as err:
        response = SiteServiceModel.get_response_error(err)
    else:
        response = SiteServiceModel.get_response_result(result)
    return response
```

* It is **elif** in python. 
* Remove dictionary key - `record_data.pop('uuid', None)` Does not raise an error but returns *None* as default.
* Had to update my tests. Apparently, unless you spell out the complete test, it is not being run. But the tests are at least  running now.
* Finally got the industry list to work correctly. Now can update and enable them. On the industry, we allow editing an industry if it is not enabled. Once enabled, it can't be edited. Don't really check for that in the backend. Should put in a check for that. But I'm done with the industry list for now. Going to work on the settings part. Trying to make the settings part into tabs. Seems like a better idea than the drop down. Also need to change what we are storing in the settings object. Don't think we need images anymore. Another question is, do we break things up into their own columns? Since we are saving the complete record every time, don't think we need to.
* Tabs look okay. Not going to win any awards for the layout or design. Need to see which css framework will work okay with vuetify. Adding a new item to the top of a JavaScript array - `unshift`. Assume it plays hell on the memory but it looks better.
* Updated create scripts for database. Now need to work on authentication and security to make sure that works okay.
* Going to work on authguard and aws amplify again. What do I need to notify when things change?
* Going to attempt to get the current session and get the necessary token to auth with our api gateway service. Still not really clear which service is best for this.
* `(await Auth.currentSession()).idToken.jwtToken` - Getting the cognito jwtToken for authorisation with the API gateway.
* Instructions for updating api server
	* Pull in changes `git pull origin master`
	* stop uwsgi - `uwsgi --stop /tmp/lookfindme.pid`
	* Update database - *tools/database* `gradle migrate`
	* start uwsgi - `uwsgi --ini uwsgi.ini --plugin python3`
	* restart nginx - `sudo /etc/init.d/nginx restart`
* Major rxjs magic to include a call to the auth server before calling our api gateway server.

```typescript
  return GetCurrentSession$().pipe(
    switchMap( (data) => ajax(
      {
        method: reqMethod,
        url: reqUrl,
        body: reqBody,
        headers: Object.assign({}, {'Content-Type': 'application/json', 'Authorization': data.idToken.jwtToken}, reqHeaders)
      }
    ).pipe(
      tap ( data => logger.debug('ajax response', data)),
      map (data => data.response.result))
    )
```
Going to build it and see if it works.

## Tuesday 19 June 2018
I'm the hell knowns as CORS. Trying to access the backend application but have to configure CORS to allow access. Getting a list of known/required headers is a nightmare. Plus, API Gateway CORS support should only be enabled after you get CORS working with your application. It's a freaking nightmare.
I did this once when I built the Wordpress plugin. Will see if I have any notes related to that.
[Wordpress Header Notes](http://www.catenare.com/devnotes/php/wordpress/notes/#api-notes) - Notes related to me working on a PHP wordpress project related to headers.  

* Creating a decorator in python
	* [Python Decorators](https://python-3-patterns-idioms-test.readthedocs.io/en/latest/PythonDecorators.html) - [Primer on Python Decorators](https://realpython.com/primer-on-python-decorators/)
	* Using jupyter notebook to walk through it.
	* Actually created a separate notebook. Think I have the hang of it.

```python
def add_headers(response_function):
    def wrapper(*args, **kwargs):
        headers = response_function(*args, **kwargs)
        headers['extra'] = '1'
        print(headers)
#         return response_function(*args, **kwargs)
        return headers
    return wrapper

@add_headers
def response_function():
    result = {'hello': 'World'}
    return result

# demo_function = add_headers(response_function)
# print(demo_function())
print(response_function())
```

My Code

```python
@add_headers
def get_response_result(result, code=200):
    response = make_response(jsonify({'result': result}), code)
    return response


def get_response_error(result="An error occurred", code=400):
    response = make_response(jsonify({'error': str(result)}), code)
    return response

def add_headers(response_function):
    def wrapper(*args, **kwargs):
        response = response_function(*args, **kwargs)
        response.headers['Content-Type'] = 'application/json'
        response.headers['Access-Control-Allow-Origin'] = '*'
        response.headers['Access-Control-Allow-Headers'] = 'Authorization, Content-Type'
        response.headers['Access-Control-Allow-Credentials'] = True
        return response
    return wrapper
```

* In Python, function order matters. Can't call a function before it is defined.
* So, CORS functionality actually takes the response from the request and returns the origin based on that request. Mmmm.
* Look into logging when I get back.
* How to resolve this CORS issue?
	* Client is sending headers to the server which the server needs to respond to.
	* It's and OPTION call which means we need to reply to that call.
	* Don't know if the ajax observable is sending things I don't know about.
	* Need to setup logging for Python so I can log what is happening.
	* Fixing the issue
		- [x] Setup logging for Python
				* Can at least tell which functions are being called.
				* Going with flask_cors. Still having issues. Can't seem to be able to save anything. Used to work via a proxy.
		- [x] See what is being sent in the headers when the client connects to the server. Using `curl -i -X OPTIONS`
		- [x] See what we are sending back.
			- [x] Decorator is not working because I'm sending back a result rather than a function that produces a result.
	* *curl* to find out if we are getting the right headers back.
		* `curl -i -X OPTIONS` include header information

* Sending Post Data via curl

```
curl --header "Content-Type: application/json" \
  --request POST \
  --data '{"username":"xyz","password":"xyz"}' \
  http://localhost:3000/api/login
```

		* Shows what header information is being returned.
	* Need to get a generic setup to return for any option request.
	* Fixed an issue where the loader wasn't going away during an error. Resolved now.
	* Seems to resolved on my local machine. Installed `axios` but didn't seem to be necessary.

* JavaScript code that seems to work

```javascript
const executeAjax$ = (reqMethod, reqUrl, reqBody=null, reqHeaders={}) => {

  return GetCurrentSession$().pipe(
    switchMap( (data) => ajax(
      {
        method: reqMethod,
        url: reqUrl,
        body: reqBody,
        crossDomain: false,
        withCredentials: false,
        headers: Object.assign({}, {'Content-Type': 'application/json'},{'Authorization': data.idToken.jwtToken}, reqHeaders)
      }
    ).pipe(
      catchError( err => of(err)),
      tap ( data => logger.debug('ajax response', data)),
      map ( (data: any) => data.response.result))
    )
  )

  };
```

* Configuration for python side - *Notice the CORS* 

```python
def create_app():
    app = Flask(__name__)
    CORS(app, expose_headers='Authorization')
    import app.routes.test as test_route
    import app.routes.admin as admin_route
    import app.routes.site as site_route
    import app.routes.user as user_route
    app.register_blueprint(test_route.bp)
    app.register_blueprint(admin_route.bp)
    app.register_blueprint(site_route.bp)
    app.register_blueprint(user_route.bp)
    return app
```

Spent all day trying to get CORS to work. Was fighting with the client and the backend server. Seems that everything is related to the FLASK/python application sending the correct headers back to the web client. Ended up using flask-cors. Seems like it already does all the dirty work I need to do. When one is doing functions, one has to keep that in mind.

- [x] Getting import roles to work
	- [x] Get the all setup to work too. 

* Issue I'm running into now. ** 'Access-Control-Allow-Origin' header in the response must not be the wildcard '*' **. See if I can get ngrok to work. Who knows.

* On Amazon API Gateway. Enabled CORS
	* Access-Control-Allow-Headers: true
	* OPTIONS there too.
* On the client
	* withCredentials: true
	* Added Authorization Header
	* Leaving crossDomain as false
* Creating a new API from scratch. I'm worried that the CORS stuff is all messed up.
* Hardest part is getting the domain redirected to the new domain name. Nothing is ever just straightforward. Think the issue I'm having right now is that the backend server is returning "*" in the content header. These headers are a mess.
* So, when you delete your API and you also deleted the custom domain, it seems that the only way to create a new one with the same domain name is to remove that domain from your dns and then recreate.
* Ok. Deleted the cname record from GoDaddy and was able to recreate the custom domain name. Now just have to wait for it to initialise. That takes forever. In the meantime, going to set the url to ngrok to see if we can get that to work. Might need to have some type of webhook to determine which origin header to use.
* Configuring flask-cors to only allow from a specific domain name. - [Flask CORS Documentation](https://flask-cors.corydolphin.com/en/latest/index.html) - Might have to not use this anymore. Seems like I may have found a solution that works better. We will see.

```python
    CORS(app, expose_headers='Authorization', origins=['*.lookfindme.com', '*.ngrok.io'], supports_credentials=True)
```

* Side note - added `PIP_NO_BINARY=psycopg2` to *.flaskenv* file. Hoping that will stick so pipenv doesn't install the wrong version of psycopg2 that keeps sending out an error message.

### ngrok config - [Documentation](https://ngrok.com/docs#tunnel-definitions)
* Creating an *ngrok.yml* file in the api folder. Run both services via ngrok in the *eu* region.
* Start command - `ngrok start -config=./ngrok.yml --all`

```yaml
region: eu  
tunnels:
  api:
    proto: http
    addr: 5000
    bind_tls: true
  admin:
    proto: http
    addr: 8080
    host_header: "localhost:8080"
    bind_tls: true
```

* Think we finally resolve the CORS issue. Ended up with using a flask after configuration to get everything going the way we want. Need to put the code here. Restarted visual studio code because it was running really slow. Added the code below to my create_app() function for creating flask app

```python
    @app.after_request
    def after_request(response):
        response.headers.add('Access-Control-Allow-Origin', "https://2a9cc487.eu.ngrok.io")

        response.headers.add('Access-Control-Allow-Headers', 'Content-Type,Authorization,X-Requested-With')
        response.headers.add('Access-Control-Allow-Credentials', 'true')
        response.headers.add('Access-Control-Allow-Methods', 'GET,PUT,POST,DELETE')
        return response
```

* list of headers to configure

```php
$origin=isset($_SERVER['HTTP_ORIGIN'])?$_SERVER['HTTP_ORIGIN']:$_SERVER['HTTP_HOST'];
header('Access-Control-Allow-Origin: '.$origin);		
header('Access-Control-Allow-Methods: POST, OPTIONS, GET, PUT');
header('Access-Control-Allow-Credentials: true');
header('Access-Control-Allow-Headers: Authorization, X-Requested-With');
header('P3P: CP="NON DSP LAW CUR ADM DEV TAI PSA PSD HIS OUR DEL IND UNI PUR COM NAV INT DEM CNT STA POL HEA PRE LOC IVD SAM IVA OTC"');
header('Access-Control-Max-Age: 1');
```

* We finally have a solution that includes dynamically adding a CORS Access-Control-Allow-Origin header.
```python
"""Main Flask App"""
from flask import Flask, request
from app.config.settings import config

ALLOWED_URLS = config('ALLOWED_URLS').split("|")

def create_app():
    app = Flask(__name__)

    import app.routes.test as test_route
    import app.routes.admin as admin_route
    import app.routes.site as site_route
    import app.routes.user as user_route
    app.register_blueprint(test_route.bp)
    app.register_blueprint(admin_route.bp)
    app.register_blueprint(site_route.bp)
    app.register_blueprint(user_route.bp)
                                                                
    @app.after_request
    def after_request(response):
        origin = request.headers['Origin']

        result = list(
            filter(
                lambda x: x in origin, 
                ALLOWED_URLS
            )
        )

        if len(result) > 0:
            response.headers.add('Access-Control-Allow-Origin', origin)

        response.headers.add('Access-Control-Allow-Headers', 'Content-Type,Authorization,X-Requested-With')
        response.headers.add('Access-Control-Allow-Credentials', 'true')
        response.headers.add('Access-Control-Allow-Methods', 'GET,PUT,POST,DELETE')
        return response

    return app
```

Solution source - [CORS, AngularJS and Flask](http://corpus.hubwiz.com/2/angularjs/23741362.html)

* Depends on the *request* being a global object. Using a filter to see if the domain name is in the origin url. Gives some security and allow for domain level access. Means I will use ngrok to access remote site. Now to test the authentication part. Seems like a better solution than the CORS solution.

* Still not able to get the authorization to work on the API Gateway. Might have to resort to just checking it on the actual server side. To do tomorrow.
## Wednesday 19 June 2017
Another day of trying to get authorization to work. It works with Postman so it has nothing to do with the other issues. Need to figure out why it works with Postman but not with the actual application.

* Using Postman to troubleshoot application authorisation.
* `ngrok start -config=./ngrok.yml --all` 
* `alias ngrok-start="ngrok start -config=./ngrok.yml --all"`
    * [Bash Programming](http://tldp.org/HOWTO/Bash-Prog-Intro-HOWTO-2.html#ss2.1) - Make into one liners.
    * Really want aliases. [Aliases in Bash](https://davidwalsh.name/alias-bash)
    * Productivity with Bash [Bash Productivity](http://www.caliban.org/bash/index.shtml)

```bash
# alias-name='command to do thing'

alias docker-refresh='docker-compose down && docker-compose up'
alias serve-dir='python -m SimpleHTTPServer'
```

* Testing configuration with ngrok and Postman.
    * Created test api that points back to local running api server via ngrok.
    * Client server accessible via ngrok too.
    - [x] Eliminate any issues with the API server
    - [x] Issue with getting Origin header. Error is KeyError: 'HTTP_ORIGIN'
        - [x] Try and send back the Origin header. Setup the header in the Request section. Then setup the response in the integration section. Might have to save and then try again if using the console. Does not seem to make any difference though.
            - [x] Setting it in the Method Request. **Does not work**
            - [x] Setting up and integration mapping - To get anything sent to the backend, Setup in both the method and the request integration section
    - [x] API Gateway with authorization key works. Tested with Postman. Issue is now related to the code we are sending to the API Gateway.
* Troubleshooting the client
    - [x] Removing the extra headers. Only leaving the Authorization header. 
        - [x] Removing the Content-Type header seems to want to submit the data as a form. 
        - [x] Putting the content-type header back. Removed my fancy function to create the header object with Object.assign({}). Header is `headers: {'Content-Type': 'application/json','Authorization': data.idToken.jwtToken}`
        - [x] Really slow because I'm dealing with a slow proxy connection from my local machine.
    - [x] Added CORS to API gateway. Added explicit origin server. Also added *X-Requested-With* to *Access-Control-Allow-Headers*
    - [x] ***It works***
* It is all about the headers. CORS is a pain. Unfortunately, would have loved to use flask-cors but it would require me to learn that code before I could even use it. Documentation is great but it seems very specific. 

* Headers we had to add
    * **Access-Control-Allow-Headers* - *X-Requested-With*
    * Has to be very explicit with the Origin header.
    * Need to return a specific header.
    * Use OPTIONS in amazon to essentially notify the client with all the data it needs.

* [List of Header Fields](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields#cite_note-CORS-8)
* Authorization key works just fine when sent from Postman. Also fixed the issue with the HTTP_ORIGIN key issue. Now essentially catch an error and replace it with host. Assuming that is being controlled by Amazon not sending back all the headers. Could try and see if I can get the Origin header sent.
* [AWS API Gateway Integration Pass-through-behavior](https://docs.aws.amazon.com/apigateway/latest/developerguide/integration-passthrough-behaviors.html)

### Main lookfindme site.
* Trying to pull front data from database. Any changes made in admin section will appear in front section.
* Need to update everything first. It's been a few weeks since I've worked with that site.
* Think everything is being pulled from an outside config file anyway.
* Updating my environment. Reinstall psycopg2 with the notes about export 

```bash
export PIP_NO_BINARY=psycopg2
pipenv install psycopg2
```

Just found out that in medics, this creates the ability to copy the code that is inside. Nice!

* Updating all the code in lookfindme. Probably going to have to spend some time just cleaning everything up. Will then create an object with all the details from the settings. That's the main page. Also get the list of memberships and the list of industries. Sounds like I should save all of that stuff in a dynamodb field with the ability to just save new ones as the become available. Would then pull the data from the dynamodb field. Can setup dynamodb locally and see if I can get it to work. Who knows?
* My attempt at writing a decorator. Added new response headers to a response. Found an easier way to do it with *@app.after_request* and *flask.request* which is a global. Solved the CORS issue.

```python
def add_headers(response_function):

    @wraps(response_function)
    def wrapper(*args, **kwargs):
        response = response_function(*args, **kwargs)
        response.headers['Content-Type'] = 'application/json'
        response.headers['Access-Control-Allow-Origin'] = 'https://2a9cc487.eu.ngrok.io'
        response.headers['Access-Control-Allow-Headers'] = 'Authorization, Content-Type'
        response.headers['Access-Control-Allow-Credentials'] = 'true'
        response.headers['Access-Control-Allow-Headers'] = 'Content-Type,Authorization,X-Requested-With'
        
        def new_response_function(*args, **kwargs):
            return response

        return response
    return wrapper
```

* Got the basic endpoint for the public api created. Tests also created and they work. Now it is time to set it up on the actual client side. Going to use axios since it is already installed.
* Everything is getting really slow. Just trying to update the front page. It is taking forever.
* Redoing my css extract. Installing `npm install --save-dev mini-css-extract-plugin` Will need to reconfigure to get it to work with the current setup. Current setup is just jacked.
* Hopefully got everything working. We are about to find out.
    * Installed vue-loader and vue-style-loader. Hope it works.
    * Got the basic site to work. Have FAQ and About working on the site. Even the main image can be changed.
* Trying to fix the build issues. Got the site to upload. Now working. But images are not working. Will have to fix that.
* Updated the front page to talk to the main server. Need to add a button to clear image list.
* Running admin site and public site at the same time.

## Thursday 21 June 2018
Got the basic admin site connected to the public site. Just need to redo the formatting/design of the site. Also need to make the  transitions better. Going to focus today on the KinderCare site.

- [ ] Setup security to backend server (certificate). Will have to configure certificate to only work on specific endpoints.
- [ ] Setup Cognito for username/password acces
    - [ ] Will use the same Cognito for parent/guardian access in the future.
    - [ ] Registration should include email/first/last/phone
    - [ ] Site will be added based on which site you are registering from.
    - [ ] Need a child's id number to validate you are eligible to register for the site.
- [ ] Create username/password screens.
    - [ ] New password
    - [ ] Reset password
    - [ ] Verification code
Did not really get anything done today. Did write an article for my blog that needs to be edited and updated. Should probably check the rest of the articles and check for errors.

Need to update my blog to work correctly on a mobile phone or device. Fix the form to fill the whole space on a mobile device. It seems to be okay on the desktop browser. Have to get it to work on iPad browser.
Was unable to configure NGINX correctly with a path of /wordpress. Luckily the API works connecting directly to the server. Now need to clean up the bottom form.

Ok. Cleaned up the bottom part of my site. Uploading this version. Going to add extract text to it. Seems to be working really well. Uses style-loader during development. ExtractCss when actually building for deployment.