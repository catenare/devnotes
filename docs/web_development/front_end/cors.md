# Fixing *Access-Control-Allow-Origin* issue with Flask

* [Developer Notebook Link](https://www.catenare.com/devnotes/api/CORS%20with%20FLASK%20without%20Flask-CORS/)

* What is CORS?   
[Understanding CORS](https://spring.io/understanding/CORS) - Pivotal Spring Article.

Accessing the Flask based API with *Postman* works, using *Curl* works, but it fails when connecting with your web application. (It worked just fine locally using the webpack proxy.) Checking the console shows an *Access-Control-Allow-Origin* error. Welcome to CORS or how to convince the browser to trust your API server.

One option with Flask is to use [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/). It works fine until you decide to setup authorisation with your Amazon API Gateway. Now the browser complains that *Access-Control-Allow-Origin* cannot be set to "\*". Since this API will be accessed by multiple web applications with different domain names, having one location configured does not work. Fastest solution for me was to configure the response headers directly with Flask. Just use the **@app.after_request** decorator and the global *request* object.

**@app.after_request** runs after every request, even if you're using Blueprints. Because **request** is a global object,  the request headers are available in the decorator function. This includes the *Origin* header which points to the web application server. 

Create a function with the **@app.after_request** decorator. In the function, include a list of allowed domains to verify the web servers allowed to access the API. If allowed, that server is set as the Origin in the *Access-Control-Allow-Origin* header. The response headers now has a specific Origin returned.

Unfortunately, using Amazon's API Gateway to authorize client access removes the *Origin* header. To fix, include a check for the *Host* header if the *Origin* header is not available. Code is below. 

[Original Code Source](http://corpus.hubwiz.com/2/angularjs/23741362.html)

```python
from flask import Flask, request
from app.config.settings import config

ALLOWED_URLS = config('ALLOWED_URLS').split("|")

def create_app():
    app = Flask(__name__)

    import app.routes.test as test_route
    import app.routes.admin as admin_route
    import app.routes.site as site_route
    import app.routes.user as user_route
    import app.routes.public as public_route
    app.register_blueprint(test_route.bp)
    app.register_blueprint(admin_route.bp)
    app.register_blueprint(site_route.bp)
    app.register_blueprint(user_route.bp)
    app.register_blueprint(public_route.bp)
    
    # After Request function
    @app.after_request
    def after_request(response):
        try:
            origin = request.headers['Origin']
        except KeyError as err:
            app.logger.debug(err)
            origin = request.headers['Host']


        result = list(
            filter(
                lambda x: x in origin,
                ALLOWED_URLS
                )
            )

        if len(result) > 0:
            response.headers.add('Access-Control-Allow-Origin', origin)
        else:
            response.headers.add('Access-Control-Allow-Origin', '*')

        response.headers.add('Access-Control-Allow-Headers', 'Content-Type,Authorization,X-Requested-With')
        response.headers.add('Access-Control-Allow-Credentials', 'true')
        response.headers.add('Access-Control-Allow-Methods', 'GET,PUT,POST,DELETE')
        return response

    return app
```


