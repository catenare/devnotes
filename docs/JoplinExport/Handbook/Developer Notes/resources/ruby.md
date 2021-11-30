---
title: ruby
updated: 2020-09-10 22:07:13Z
created: 2020-09-10 22:07:13Z
---

# Ruby Notes

## RVM Notes
* Using RVM to install Ruby after upgrading OS x
    * Error message: ```dyld: Symbol not found: _clock_gettime```
    * Solution __This worked for me__: ```xcode-select --install``` - Installed command line clients from os x.
* **No GPG software exists to validate rvm-installer, skipping.**
    * Check gnupg2 installed
        * Mac OS X - `sudo port install gnupg2`
        * *Remove link to `/opt/local/bin/gpg` used to fix an earlier issue*

## Gem
* Unable to run a command from a gem when installed with *gem install*
    * Example: *gem install cocoapods*. Expect to use *pod* as a commandline client.
    * Solution: **rvm use ruby-{current}**
    * Problem related to rvm not setting up a default ruby.

* *Warning! PATH is not properly set up*
    * [About bash_profile and bashrc on Mac OS X](http://scriptingosx.com/2017/04/about-bash_profile-and-bashrc-on-macos/) - Terminal runs .bash_profile on new window.
    * Edit *.profile*
        * Add line to beginning of file. `[[ -s "$HOME/.bash_profile" ]] && source "$HOME/.bash_profile" # Load the default .bash_profile`
```bash
# MacPorts Installer addition on 2016-08-29_at_10:22:24: adding an appropriate PATH variable for use with MacPorts.
export PATH="/opt/local/bin:/opt/local/sbin:$PATH"
# Finished adapting your PATH environment variable for use with MacPorts.

export NVM_DIR="/Users/themartins/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"  # This loads nvm

export WORKON_HOME=~/Envs
export VIRTUALENVWRAPPER_SCRIPT=$HOME/Library/Python/3.6/bin/virtualenvwrapper.sh
source "$HOME/Library/Python/3.6/bin/virtualenvwrapper_lazy.sh"
export PATH="$HOME/Library/Python/3.6/bin:$PATH"

# pip bash completion start
_pip_completion()
{
    COMPREPLY=( $( COMP_WORDS="${COMP_WORDS[*]}" \
                   COMP_CWORD=$COMP_CWORD \
                   PIP_AUTO_COMPLETE=1 $1 ) )
}
complete -o default -F _pip_completion pip
# pip bash completion end

export PATH="$PATH:$HOME/.local/bin"

alias mongostart="sudo mongod -f /opt/local/etc/mongodb/mongod.conf --httpinterface --rest"

mongostop_func () {
	local mongopid = `less /opt/local/var/db/mongodb/mongod.lock`;
	if [[ $mongopid =~ [[:digit:]] ]]; then
		sudo kill -15 $mongopid;
		echo mongod process $mongopid terminated;
	else
		echo mongo process $mongopid not exists;
	fi
}

alias mongostop="mongostop_func"

export LC_ALL=en_US.UTF-8
export LANG=en_US.UTF-8

echo ".profile loaded"


```
* Edit *.bash_profile*
```bash
[[ -s "$HOME/.profile" ]] && source "$HOME/.profile" # Load the default .profile
# export NVM_DIR="$HOME/.nvm"
# [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" # This loads nvm

# Export libsass library
export SASS_LIBSASS_PATH=/Users/themartins/Projects/Tools/libsass

export PATH="$HOME/Library/Python/3.6/bin:$PATH"
eval $(/usr/libexec/path_helper -s)

# export PATH="/Users/themartins/Documents/Projects/tutorial:$PATH"
export PATH=$PATH:"~/.bin"

# export JAVA_HOME="/Library/Java/JavaVirtualMachines/jdk1.8.0_131.jdk/Contents/Home"
export JAVA_HOME="/Library/Java/JavaVirtualMachines/jdk-9.jdk/Contents/Home"
export ANDROID_HOME="/Users/themartins/Library/Android/sdk"
export PATH=$ANDROID_HOME:$PATH

###-tns-completion-start-###
if [ -f /Users/themartins/.tnsrc ]; then 
    source /Users/themartins/.tnsrc 
fi
###-tns-completion-end-###

export PATH=$PATH:/Users/themartins/bin

source '/Users/themartins/lib/azure-cli/az.completion'

# echo "end .bash_profile"

#THIS MUST BE AT THE END OF THE FILE FOR SDKMAN TO WORK!!!
export SDKMAN_DIR="/Users/themartins/.sdkman"
[[ -s "/Users/themartins/.sdkman/bin/sdkman-init.sh" ]] && source "/Users/themartins/.sdkman/bin/sdkman-init.sh"

export PATH="$PATH:$HOME/.rvm/bin"
[[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm" # Load RVM into a shell session *as a function*
```
