# Developer Notes for Johan Martin [martin.johan@johan-martin.com](mailto:martin.johan@johan-martin.com)
Notes of what I find/learn/realize as I work on different projects. Good place to write them down.

## Git
* Git error message. Can't merge unrelated histories.
* Allow unrelated histories [StackOverflow Issue](http://stackoverflow.com/questions/37937984/git-refusing-to-merge-unrelated-histories)
  * git pull remote branch --allow-unrelated-histories

* Git error trying to push when pull seems to work

```
hint: Updates were rejected because a pushed branch tip is behind its remote
hint: counterpart. Check out this branch and integrate the remote changes
hint: (e.g. 'git pull ...') before pushing again.
```
* *Hint:* **Read hints**
  * Checkout out rejected branch. ```git checkout master```
  * ```git pull {remote} master --allow-unrelated-histories```
  * Fix conflicts and commit
  * ```git push {remote} master```

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

# Sass
* Compiling compass sass with sass c library.
	* *sass --compass sass/styles.scss test,css* - seems to read the compass config.rb file to find paths.

# RVM and ruby
* Unable to run a command from a gem when installed with *gem install*
  * Example: *gem install cocoapods*. Expect to use *pod* as a commandline client.
  * Solution: **rvm use ruby-{current}**
  * Problem related to rvm not setting up a default ruby.
# Downloading files with wget
* Use ```wget -c``` or ```wget --continue``` to restart a stopped or aborted download