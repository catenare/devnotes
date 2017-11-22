# Local Setup

## Terminal 
* .bash_profile
```bash
[[ -s "$HOME/.profile" ]] && source "$HOME/.profile" # Load the default .profile


# Export libsass library
export SASS_LIBSASS_PATH=/Users/themartins/Projects/Tools/libsass

export PATH=$PATH:"~/.bin"

export PATH=$PATH:/Users/themartins/bin

#THIS MUST BE AT THE END OF THE FILE FOR SDKMAN TO WORK!!!
export SDKMAN_DIR="/Users/themartins/.sdkman"
[[ -s "/Users/themartins/.sdkman/bin/sdkman-init.sh" ]] && source "/Users/themartins/.sdkman/bin/sdkman-init.sh"

export PATH="$PATH:$HOME/.rvm/bin"
[[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm" # Load RVM into a shell session *as a function*
```
* .profile
```bash
# MacPorts Installer addition on 2016-08-29_at_10:22:24: adding an appropriate PATH variable for use with MacPorts.
export PATH="/opt/local/bin:/opt/local/sbin:$PATH"
# Finished adapting your PATH environment variable for use with MacPorts.

export NVM_DIR="/Users/themartins/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"  # This loads nvm

# virtualenvwrappers
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

export PATH="$PATH:$HOME/.local/bin" #ngrok

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
