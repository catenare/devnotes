# Developer Notes for Johan Martin
## martin.johan@johan-martin.com

# Notes of what I find/learn/realize as I work on different projects. Good place to write them down.

## Git
* Git error message. Can't merge unrelated histories.
* Allow unrelated histories [StackOverflow Issue](http://stackoverflow.com/questions/37937984/git-refusing-to-merge-unrelated-histories)
* git pull remote branch --allow-unrelated-histories

# Python
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
## Other
* Terminal all screwed up after using python repl
	* ~~Install python readline **pip install readline**.~~ Does not seem to work because installed in user space.
	* Using macports. Installed ***py35-readline***. That seemed to work.

# Github Markdown
* Languages for code blocks - [highlights.js](https://highlightjs.org/static/demo/)
* Emoji List - :bowtie [Emoji Cheat Sheet](http://www.webpagefx.com/tools/emoji-cheat-sheet/)
