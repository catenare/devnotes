# Using Python Notes

## Resources
* [Fullstack Python](https://www.fullstackpython.com/)
* Podcasts
    * [Talk Python To Me](https://talkpython.fm/)
    * [Python Bytes](https://pythonbytes.fm/)

## Notices
* Using python terminal in PyCharm with virtualenv messes up the python terminal everywhere else. Need to exit PyCharm Python Terminal if I want to use the virtualenv from Mac OS X terminal.

## Pip
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

## Issue with readline
* Terminal all screwed up after using python repl
    * `sudo port install python36 +readline` - fixes issues with python and terminal Mac OS X

## Create package Resources
* [Packaging and Distributing Projects](https://packaging.python.org/tutorials/distributing-packages/) - Guide
* [setup.py cheatsheet](http://turbo87.github.io/setup.py/)
* [setup.py guide](https://github.com/kennethreitz/setup.py)

## Other issues
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

## Virtual Environments
* [VirtualEnvWrapper](https://virtualenvwrapper.readthedocs.io/en/latest/index.html)

## Setting up uswgi on Ubuntu with Flex
* Resource: [How to serve Flask Application](https://www.digitalocean.com/community/tutorials/how-to-serve-flask-applications-with-uwsgi-and-nginx-on-ubuntu-16-04)
* Packages needed.
    * `sudo apt install build-essentials python3-dev` - needed to build uswgi
* Use *virtualenv* and create virtualenv.
* Install *flask* and *uswgi*.
* Configure firewall - `sudo ufw allow 5000`
* Setup *wsgi.py*
```python
from myproject import app

if __name__ == "__main__":
    app.run()
```
* Test it: `uwsgi --socket 0.0.0.0:5000 --protocol=http -w wsgi:app`

## Special Method Names
* [Computed Attributes](http://www.diveintopython3.net/special-method-names.html) - magic names for objects
* [MagicMethods](https://rszalski.github.io/magicmethods/)

## Notes
* Jupyter Notebooks
