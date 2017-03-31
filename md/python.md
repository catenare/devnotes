# Using Python
## Pip

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
	* ~~Install python readline **pip install readline**.~~ Does not seem to work because installed in user space.
	* Using macports. Installed ***py35-readline***. That seemed to work.