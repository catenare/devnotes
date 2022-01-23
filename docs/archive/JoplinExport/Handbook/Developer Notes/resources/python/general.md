---
title: general
updated: 2020-09-10 22:07:13Z
created: 2020-09-10 22:07:13Z
---

# Using Python Notes

## Resources
* [Fullstack Python](https://www.fullstackpython.com/)
* Podcasts
    * [Talk Python To Me](https://talkpython.fm/)
    * [Python Bytes](https://pythonbytes.fm/)
* Python books online [Invent with python](http://inventwithpython.com)

## Notes
* ~~Using python terminal in PyCharm with virtualenv messes up the python terminal everywhere else. Need to exit PyCharm Python Terminal if I want to use the virtualenv from Mac OS X terminal.~~
* Reload module from REPL
    * `import imp`
    * `import.reload(module)` - module is the name of the module to reload
* Import packages from current directory
    * `from . import package` - will look in current directory for the package
* Shuffle list - random sequence for list
    * `import random`
    * `list = [a,b,c,d]`
    * `random.shuffle(list)`
    * `for item in list:`
* Issue with ASCII environment
    * [Python 3 Surrogate handling](http://click.pocoo.org/6/python3/#python-3-surrogate-handling)
    * Add to *~/.profile*
        * `export LC_ALL=en_US.UTF-8`
        * `export LANG=en_US.UTF-8`
* Special Method Names
    * [Computed Attributes](http://www.diveintopython3.net/special-method-names.html) - magic names for objects
    * [MagicMethods](https://rszalski.github.io/magicmethods/)
* Issue with readline
    * ~~Terminal all screwed up after using python repl~~
        * ~~`sudo port install python36 +readline` - fixes issues with python and terminal Mac OS X~~
* Merge dictionaries
  * `z = {**x, **y}` - [Merge Python Dictionaries](https://stackoverflow.com/questions/38987/how-to-merge-two-dictionaries-in-a-single-expression)

* uwsgi
  * wsgi = wsgi.py file
  * `uwsgi --socket 0.0.0.0:5000 --protocol=http -H /Users/themartins/Envs/lookfindmeAPI-jd3kET2g -w wsgi`
  * `uwsgi --socket 0.0.0.0:5000 --protocol=http --wsgi-file wsgi.py --callable myApp -H /Users/themartins/Envs/lookfindmeAPI-jd3kET2g`

## ~~Pip~~ **Now using pipenv**
* Upgrade pip - `pip install --upgrade pip`
* Error message: *"Can not perform a '--user' install. User site-packages are not visible in this virtualenv"*
* Problems **~/Library/Application Support/pip/pip.conf** contains **user=true**
* Resolution: Override the config in your virtualenv pip config file
	* Create **$VIRTUAL_ENV/pip.conf**
	* Place config information to override user=true
```Ini
[install]
user=false
```
* [Pip Configuration](https://pip.pypa.io/en/stable/user_guide/#configuration) | [StackOverflow Issue](http://stackoverflow.com/questions/30604952/pip-default-behavior-conflicts-with-virtualenv)
## Install
* [Installing packages](https://packaging.python.org/tutorials/installing-packages/)

### Install pip as user
* get the get-pip.py script
	* Get the script ```wget https://bootstrap.pypa.io/get-pip.py```
	* Run the script with user option ```pytoh get-pip.py --user```
* Now install all pip packages into user space. ```pip install --user <package>```

### Setup pip config file - want to set default settings for command line. Like always install in user space.
* Create file ```$HOME/Library/Application Support/pip/pip.conf```
* Edit file
```Ini
[Install]
user = true
```

## Packaging python
* [Python Packaging User Guid](https://packaging.python.org/)
* [Packaging and Distributing Projects](https://packaging.python.org/tutorials/distributing-packages/) - Guide
* [setup.py cheatsheet](http://turbo87.github.io/setup.py/)
* [setup.py guide](https://github.com/kennethreitz/setup.py)


* [VirtualEnvWrapper](https://virtualenvwrapper.readthedocs.io/en/latest/index.html)

## Uwsgi and NGINX
Notes for configuring uwsgi and Nginx
Using uwsgi to serve the python api on aws servers.
* [Digital Ocean - deploy python to wsgi](https://www.digitalocean.com/community/tutorials/how-to-deploy-python-wsgi-applications-using-uwsgi-web-server-with-nginx) - docs.

### Using uwsgi.
* Notes:
	* If api starts at /double than nginx config location should be /double
* Packages needed - Ubuntu
	* `apt install uwsgi-core uwsgi-plugin-python3` - need python3 plugin
* `pip3 --user install pipenv` - need pipenv for our application.
* Files need for uwsgi to work.
	* *wsgi.py* - startup python file to launch our application
	* *uwsgi.ini* - configuration file for our uwsgi server
	* Commands
		* `uwsgi --ini uwsgi.ini --plugin python3` - start the server on ec2. Configuration will daemonize the app. Configuration already includes the config to daemonize it.
		* `uwsgi --stop /tmp/lookfindme.pid` - stops the service.
* *wsgi.py* file
```python
from app import lookfindme
myApp = lookfindme.create_app()

if __name__ == "__main__":
  myApp.run()
```
* *uwsgi.ini* file (different local and server version)
```ini
[uwsgi]
http-socket= :9090
socket=127.0.0.1:8000
socket=/tmp/lookfindme.sock
chmod-socket=666
wsgi-file=wsgi.py
callable=myApp
master=true
processes=5
vacuum=true
virtualenv=/Users/themartins/Envs/lookfindmeAPI-jd3kET2g
daemonize=/tmp/uwsgi_daemon.log
pidfile=/tmp/lookfindme.pid
```
* *nginx.conf* - nginx config. nginx already includes uwsgi support.
```conf
upstream flask {
  server 127.0.0.1:9000;
}
server {
  listen 80 default_server;
  listen [::]:80 default_server;

    location /double {
      include /etc/nginx/uwsgi_params;
      uwsgi_pass flask;
      uwsgi_param Host $host;
      uwsgi_param X-Real-IP $remote_addr;
      uwsgi_param X-Forwarded-For $proxy_add_x_forwarded_for;
      uwsgi_param X-Forwarded-Proto $http_x_forwarded_proto;
    }
  }
```
