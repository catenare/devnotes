## MacPorts

| Alias | Command                            | Description                                                  |
|-------|------------------------------------|--------------------------------------------------------------|
| pc    | `sudo port clean --all installed`  | Clean up intermediate installation files for installed ports |
| pi    | `sudo port install`                | Install package given as argument                            |
| psu   | `sudo port selfupdate`             | Update ports tree with MacPorts repository                   |
| puni  | `sudo port uninstall inactive`     | Uninstall inactive ports                                     |
| puo   | `sudo port upgrade outdated`       | Upgrade ports with newer versions available                  |
| pup   | `psu && puo`                       | Update ports tree, then upgrade ports to newest versions     |

## iTerm2 Plugin commands

* `_iterm2_command <iterm2-command>`
  executes an arbitrary iTerm2 command via an escape code sequence.
  See https://iterm2.com/documentation-escape-codes.html for all supported commands.

* `iterm2_profile <profile-name>`
  changes the current terminal window's profile (colors, fonts, settings, etc).
  `profile-name` is the name of another iTerm2 profile. The profile name can contain spaces.

* `iterm2_tab_color <red> <green> <blue>`
  changes the color of iTerm2's currently active tab.
  `red`/`green`/`blue` are on the range 0-255.

* `iterm2_tab_color_reset`
  resets the color of iTerm2's current tab back to default.
  
  ## MacOS
  ## Commands

| Command       | Description                                              |
| :------------ | :------------------------------------------------------- |
| `tab`         | Open the current directory in a new tab                  |
| `split_tab`   | Split the current terminal tab horizontally              |
| `vsplit_tab`  | Split the current terminal tab vertically                |
| `ofd`         | Open the current directory in a Finder window            |
| `pfd`         | Return the path of the frontmost Finder window           |
| `pfs`         | Return the current Finder selection                      |
| `cdf`         | `cd` to the current Finder directory                     |
| `pushdf`      | `pushd` to the current Finder directory                  |
| `pxd`         | Return the current Xcode project directory               |
| `cdx`         | `cd` to the current Xcode project directory              |
| `quick-look`  | Quick-Look a specified file                              |
| `man-preview` | Open a specified man page in Preview app                 |
| `showfiles`   | Show hidden files in Finder                              |
| `hidefiles`   | Hide the hidden files in Finder                          |
| `itunes`      | _DEPRECATED_. Use `music` from macOS Catalina on         |
| `music`       | Control Apple Music. Use `music -h` for usage details    |
| `spotify`     | Control Spotify and search by artist, album, track…      |
| `rmdsstore`   | Remove .DS_Store files recursively in a directory        |
| `btrestart`   | Restart the Bluetooth daemon                             |
| `freespace`   | Erases purgeable disk space with 0s on the selected disk |

## NPM

| Alias   | Command                      | Description                                                     |
|:------  |:-----------------------------|:----------------------------------------------------------------|
| `npmg`  | `npm i -g`                   | Install dependencies globally                                   |
| `npmS`  | `npm i -S`                   | Install and save to dependencies in your package.json           |
| `npmD`  | `npm i -D`                   | Install and save to dev-dependencies in your package.json       |
| `npmF`  | `npm i -f`                   | Force install from remote registries ignoring local cache       |
| `npmE`  | `PATH="$(npm bin)":"$PATH"`  | Run command from node_modules folder based on current directory |
| `npmO`  | `npm outdated`               | Check which npm modules are outdated                            |
| `npmU`  | `npm update`                 | Update all the packages listed to the latest version            |
| `npmV`  | `npm -v`                     | Check package versions                                          |
| `npmL`  | `npm list`                   | List installed packages                                         |
| `npmL0` | `npm ls --depth=0`           | List top-level installed packages                               |
| `npmst` | `npm start`                  | Run npm start                                                   |
| `npmt`  | `npm test`                   | Run npm test                                                    |
| `npmR`  | `npm run`                    | Run npm scripts                                                 |
| `npmP`  | `npm publish`                | Run npm publish                                                 |
| `npmI`  | `npm init`                   | Run npm init                                                    |
| `npmi`  | `npm info`                   | Run npm info                                                    |
| `npmSe` | `npm search`                 | Run npm search                                                  |

## Pipenv
This plugin provides some features to simplify the use of Pipenv while working on ZSH. 
- Adds completion for pipenv
- Auto activates and deactivates pipenv shell
- Adds short aliases for common pipenv commands
  - `pch` is aliased to `pipenv check`
  - `pcl` is aliased to `pipenv clean`
  - `pgr` is aliased to `pipenv graph`
  - `pi` is aliased to `pipenv install`
  - `pidev` is aliased to `pipenv install --dev`
  - `pl` is aliased to `pipenv lock`
  - `po` is aliased to `pipenv open`
  - `prun` is aliased to `pipenv run`
  - `psh` is aliased to `pipenv shell`
  - `psy` is aliased to `pipenv sync`
  - `pu` is aliased to `pipenv uninstall`
  - `pwh` is aliased to `pipenv --where`
  - `pvenv` is aliased to `pipenv --venv`
  - `ppy` is aliased to `pipenv --py`

## Tmux
| Alias  | Command                | Description                                               |
| ------ | -----------------------|---------------------------------------------------------- |
| `ta`   | tmux attach -t         | Attach new tmux session to already running named session  |
| `tad`  | tmux attach -d -t      | Detach named tmux session                                 |
| `ts`   | tmux new-session -s    | Create a new named tmux session                           |
| `tl`   | tmux list-sessions     | Displays a list of running tmux sessions                  |
| `tksv` | tmux kill-server       | Terminate all running tmux sessions                       |
| `tkss` | tmux kill-session -t   | Terminate named running tmux session                      |
| `tmux` | `_zsh_tmux_plugin_run` | Start a new tmux session                                  |

## Configuration Variables

| Variable                            | Description                                                                   |
|-------------------------------------|-------------------------------------------------------------------------------|
| `ZSH_TMUX_AUTOSTART`                | Automatically starts tmux (default: `false`)                                  |
| `ZSH_TMUX_AUTOSTART_ONCE`           | Autostart only if tmux hasn't been started previously (default: `true`)       |
| `ZSH_TMUX_AUTOCONNECT`              | Automatically connect to a previous session if it exits (default: `true`)     |
| `ZSH_TMUX_AUTOQUIT`                 | Automatically closes terminal once tmux exits (default: `ZSH_TMUX_AUTOSTART`) |
| `ZSH_TMUX_FIXTERM`                  | Sets `$TERM` to 256-color term or not based on current terminal support       |
| `ZSH_TMUX_ITERM2`                   | Sets the `-CC` option for iTerm2 tmux integration (default: `false`)          |
| `ZSH_TMUX_FIXTERM_WITHOUT_256COLOR` | `$TERM` to use for non 256-color terminals (default: `screen`)                |
| `ZSH_TMUX_FIXTERM_WITH_256COLOR`    | `$TERM` to use for 256-color terminals (default: `screen-256color`            |
| `ZSH_TMUX_CONFIG`                   | Set the configuration path (default: `$HOME/.tmux.conf`)                      |
| `ZSH_TMUX_UNICODE`                  | Set `tmux -u` option to support unicode                                       |
| `ZSH_TMUX_DEFAULT_SESSION_NAME`     | Set tmux default session name when autostart is enabled                       |

## vi-mode
## Settings

- `VI_MODE_RESET_PROMPT_ON_MODE_CHANGE`: controls whether the prompt is redrawn when
  switching to a different input mode. If this is unset, the mode indicator will not
  be updated when changing to a different mode.
  Set it to `true` to enable it. For example:

  ```zsh
  VI_MODE_RESET_PROMPT_ON_MODE_CHANGE=true
  ```

  The default value is unset, unless `vi_mode_prompt_info` is used, in which case it'll
  automatically be set to `true`.

- `VI_MODE_SET_CURSOR`: controls whether the cursor style is changed when switching
  to a different input mode. Set it to `true` to enable it (default: unset):

  ```zsh
  VI_MODE_SET_CURSOR=true
  ```

- `MODE_INDICATOR`: controls the string displayed when the shell is in normal mode.
  See [Mode indicator](#mode-indicator) for details.

## Mode indicator

*Normal mode* is indicated with a red `<<<` mark at the right prompt, when it
hasn't been defined by theme.

You can change this indicator by setting the `MODE_INDICATOR` variable. This setting
supports Prompt Expansion sequences. For example:

```zsh
MODE_INDICATOR="%F{yellow}+%f"
```

You can also use the `vi_mode_prompt_info` function in your prompt, which will display
this mode indicator.

## Key bindings

Use `ESC` or `CTRL-[` to enter `Normal mode`.

NOTE: some of these key bindings are set by zsh by default when using a vi-mode keymap.

### History

- `ctrl-p` : Previous command in history
- `ctrl-n` : Next command in history
- `/`      : Search backward in history
- `n`      : Repeat the last `/`

### Vim edition

- `vv`     : Edit current command line in Vim

NOTE: this used to be bound to `v`. That is now the default (`visual-mode`).

### Movement

- `$`   : To the end of the line
- `^`   : To the first non-blank character of the line
- `0`   : To the first character of the line
- `w`   : [count] words forward
- `W`   : [count] WORDS forward
- `e`   : Forward to the end of word [count] inclusive
- `E`   : Forward to the end of WORD [count] inclusive
- `b`   : [count] words backward
- `B`   : [count] WORDS backward
- `t{char}`   : Till before [count]'th occurrence of {char} to the right
- `T{char}`   : Till before [count]'th occurrence of {char} to the left
- `f{char}`   : To [count]'th occurrence of {char} to the right
- `F{char}`   : To [count]'th occurrence of {char} to the left
- `;`   : Repeat latest f, t, F or T [count] times
- `,`   : Repeat latest f, t, F or T in opposite direction

### Insertion

- `i`   : Insert text before the cursor
- `I`   : Insert text before the first character in the line
- `a`   : Append text after the cursor
- `A`   : Append text at the end of the line
- `o`   : Insert new command line below the current one
- `O`   : Insert new command line above the current one

### Delete and Insert

- `ctrl-h`      : While in *Insert mode*: delete character before the cursor
- `ctrl-w`      : While in *Insert mode*: delete word before the cursor
- `d{motion}`   : Delete text that {motion} moves over
- `dd`          : Delete line
- `D`           : Delete characters under the cursor until the end of the line
- `c{motion}`   : Delete {motion} text and start insert
- `cc`          : Delete line and start insert
- `C`           : Delete to the end of the line and start insert
- `r{char}`     : Replace the character under the cursor with {char}
- `R`           : Enter replace mode: Each character replaces existing one
- `x`           : Delete `count` characters under and after the cursor
- `X`           : Delete `count` characters before the cursor

## Known issues

### Low `$KEYTIMEOUT`

A low `$KEYTIMEOUT` value (< 15) means that key bindings that need multiple characters,
like `vv`, will be very difficult to trigger. `$KEYTIMEOUT` controls the number of
milliseconds that must pass before a key press is read and the appropriate key binding
is triggered. For multi-character key bindings, the key presses need to happen before
the timeout is reached, so on low timeouts the key press happens too slow, and therefore
another key binding is triggered.

We recommend either setting `$KEYTIMEOUT` to a higher value, or remapping the key bindings
that you want to trigger to a keyboard sequence. For example:

```zsh
bindkey -M vicmd 'V' edit-command-line # this remaps `vv` to `V` (but overrides `visual-mode`)
```
## vscode

| Alias                   | Command                        | Description                                                                                                 |
| ----------------------- | ------------------------------ | ----------------------------------------------------------------------------------------------------------- |
| vsc                     | code .                         | Open the current folder in VS code                                                                          |
| vsca `dir`              | code --add `dir`               | Add folder(s) to the last active window                                                                     |
| vscd `file` `file`      | code --diff `file` `file`      | Compare two files with each other.                                                                          |
| vscg `file:line[:char]` | code --goto `file:line[:char]` | Open a file at the path on the specified line and character position.                                       |
| vscn                    | code --new-window              | Force to open a new window.                                                                                 |
| vscr                    | code --reuse-window            | Force to open a file or folder in the last active window.                                                   |
| vscw                    | code --wait                    | Wait for the files to be closed before returning.                                                           |
| vscu `dir`              | code --user-data-dir `dir`     | Specifies the directory that user data is kept in. Can be used to open multiple distinct instances of Code. |

## Extensions aliases

| Alias                   | Command                                                          | Description                       |
| ----------------------- | ---------------------------------------------------------------- | --------------------------------- |
| vsced `dir`             | code --extensions-dir `dir`                                      | Set the root path for extensions. |
| vscie `id or vsix-path` | code --install-extension `extension-id> or <extension-vsix-path` | Installs an extension.            |
| vscue `id or vsix-path` | code --uninstall-extension `id or vsix-path`                     | Uninstalls an extension.          |

## Other options:

| Alias        | Command                   | Description                                                                                                           |
| ------------ | ------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| vscv         | code --verbose            | Print verbose output (implies --wait).                                                                                |
| vscl `level` | code --log `level`        | Log level to use. Default is 'info'. Allowed values are 'critical', 'error', 'warn', 'info', 'debug', 'trace', 'off'. |
| vscde        | code --disable-extensions | Disable all installed extensions.                                                                                     |

## git

| Alias                | Command                                                                                                                          |
|:---------------------|:---------------------------------------------------------------------------------------------------------------------------------|
| g                    | git                                                                                                                              |
| ga                   | git add                                                                                                                          |
| gaa                  | git add --all                                                                                                                    |
| gapa                 | git add --patch                                                                                                                  |
| gau                  | git add --update                                                                                                                 |
| gav                  | git add --verbose                                                                                                                |
| gap                  | git apply                                                                                                                        |
| gapt                 | git apply --3way                                                                                                                 |
| gb                   | git branch                                                                                                                       |
| gba                  | git branch -a                                                                                                                    |
| gbd                  | git branch -d                                                                                                                    |
| gbda                 | git branch --no-color --merged \| grep -vE "^([+*]\|\s*($(git_main_branch)\|$(git_develop_branch))\s*$)" \| xargs git branch -d 2>/dev/null |
| gbD                  | git branch -D                                                                                                                    |
| gbl                  | git blame -b -w                                                                                                                  |
| gbnm                 | git branch --no-merged                                                                                                           |
| gbr                  | git branch --remote                                                                                                              |
| gbs                  | git bisect                                                                                                                       |
| gbsb                 | git bisect bad                                                                                                                   |
| gbsg                 | git bisect good                                                                                                                  |
| gbsr                 | git bisect reset                                                                                                                 |
| gbss                 | git bisect start                                                                                                                 |
| gc                   | git commit -v                                                                                                                    |
| gc!                  | git commit -v --amend                                                                                                            |
| gcn!                 | git commit -v --no-edit --amend                                                                                                  |
| gca                  | git commit -v -a                                                                                                                 |
| gca!                 | git commit -v -a --amend                                                                                                         |
| gcan!                | git commit -v -a --no-edit --amend                                                                                               |
| gcans!               | git commit -v -a -s --no-edit --amend                                                                                            |
| gcam                 | git commit -a -m                                                                                                                 |
| gcas                 | git commit -a -s                                                                                                                 |
| gcasm                | git commit -a -s -m                                                                                                                  |
| gcsm                 | git commit -s -m                                                                                                                 |
| gcb                  | git checkout -b                                                                                                                  |
| gcf                  | git config --list                                                                                                                |
| gcl                  | git clone --recurse-submodules                                                                                                   |
| gccd                 | git clone --recurse-submodules "$@" && cd "$(basename $_ .git)"                                                                  |
| gclean               | git clean -id                                                                                                                    |
| gpristine            | git reset --hard && git clean -dffx                                                                                              |
| gcm                  | git checkout $(git_main_branch)                                                                                                  |
| gcd                  | git checkout $(git_develop_branch)                                                                                               |
| gcmsg                | git commit -m                                                                                                                    |
| gco                  | git checkout                                                                                                                     |
| gcor                 | git checkout --recurse-submodules                                                                                                |
| gcount               | git shortlog -sn                                                                                                                 |
| gcp                  | git cherry-pick                                                                                                                  |
| gcpa                 | git cherry-pick --abort                                                                                                          |
| gcpc                 | git cherry-pick --continue                                                                                                       |
| gcs                  | git commit -S                                                                                                                    |
| gd                   | git diff                                                                                                                         |
| gdca                 | git diff --cached                                                                                                                |
| gdcw                 | git diff --cached --word-diff                                                                                                    |
| gdct                 | git describe --tags $(git rev-list --tags --max-count=1)                                                                         |
| gds                  | git diff --staged                                                                                                                |
| gdt                  | git diff-tree --no-commit-id --name-only -r                                                                                      |
| gdnolock             | git diff $@ ":(exclude)package-lock.json" ":(exclude)&ast;.lock"                                                                 |
| gdup                 | git diff @{upstream}                                                                                                             |
| gdv                  | git diff -w $@ \| view -                                                                                                         |
| gdw                  | git diff --word-diff                                                                                                             |
| gf                   | git fetch                                                                                                                        |
| gfa                  | git fetch --all --prune                                                                                                          |
| gfg                  | git ls-files \| grep                                                                                                             |
| gfo                  | git fetch origin                                                                                                                 |
| gg                   | git gui citool                                                                                                                   |
| gga                  | git gui citool --amend                                                                                                           |
| ggf                  | git push --force origin $(current_branch)                                                                                        |
| ggfl                 | git push --force-with-lease origin $(current_branch)                                                                             |
| ggl                  | git pull origin $(current_branch)                                                                                                |
| ggp                  | git push origin $(current_branch)                                                                                                |
| ggpnp                | ggl && ggp                                                                                                                       |
| ggpull               | git pull origin "$(git_current_branch)"                                                                                          |
| ggpur                | ggu                                                                                                                              |
| ggpush               | git push origin "$(git_current_branch)"                                                                                          |
| ggsup                | git branch --set-upstream-to=origin/$(git_current_branch)                                                                        |
| ggu                  | git pull --rebase origin $(current_branch)                                                                                       |
| gpsup                | git push --set-upstream origin $(git_current_branch)                                                                             |
| ghh                  | git help                                                                                                                         |
| gignore              | git update-index --assume-unchanged                                                                                              |
| gignored             | git ls-files -v \| grep "^[[:lower:]]"                                                                                           |
| git-svn-dcommit-push | git svn dcommit && git push github $(git_main_branch):svntrunk                                                                   |
| gk                   | gitk --all --branches &!                                                                                                          |
| gke                  | gitk --all $(git log -g --pretty=%h) &!                                                                                           |
| gl                   | git pull                                                                                                                         |
| glg                  | git log --stat                                                                                                                   |
| glgp                 | git log --stat -p                                                                                                                |
| glgg                 | git log --graph                                                                                                                  |
| glgga                | git log --graph --decorate --all                                                                                                 |
| glgm                 | git log --graph --max-count=10                                                                                                   |
| glo                  | git log --oneline --decorate                                                                                                     |
| glol                 | git log --graph --pretty='%Cred%h%Creset -%C(auto)%d%Creset %s %Cgreen(%ar) %C(bold blue)<%an>%Creset'                           |
| glols                | git log --graph --pretty='%Cred%h%Creset -%C(auto)%d%Creset %s %Cgreen(%ar) %C(bold blue)<%an>%Creset' --stat                    |
| glod                 | git log --graph --pretty='%Cred%h%Creset -%C(auto)%d%Creset %s %Cgreen(%ad) %C(bold blue)<%an>%Creset'                           |
| glods                | git log --graph --pretty='%Cred%h%Creset -%C(auto)%d%Creset %s %Cgreen(%ad) %C(bold blue)<%an>%Creset' --date=short              |
| glola                | git log --graph --pretty='%Cred%h%Creset -%C(auto)%d%Creset %s %Cgreen(%ar) %C(bold blue)<%an>%Creset' --all                     |
| glog                 | git log --oneline --decorate --graph                                                                                             |
| gloga                | git log --oneline --decorate --graph --all                                                                                       |
| glp                  | git log --pretty=\<format\>                                                                                                      |
| gm                   | git merge                                                                                                                        |
| gmom                 | git merge origin/$(git_main_branch)                                                                                              |
| gmtl                 | git mergetool --no-prompt                                                                                                        |
| gmtlvim              | git mergetool --no-prompt --tool=vimdiff                                                                                         |
| gmum                 | git merge upstream/$(git_main_branch)                                                                                            |
| gma                  | git merge --abort                                                                                                                |
| gp                   | git push                                                                                                                         |
| gpd                  | git push --dry-run                                                                                                               |
| gpf                  | git push --force-with-lease                                                                                                      |
| gpf!                 | git push --force                                                                                                                 |
| gpoat                | git push origin --all && git push origin --tags                                                                                  |
| gpr                  | git pull --rebase                                                                                                                |
| gpu                  | git push upstream                                                                                                                |
| gpv                  | git push -v                                                                                                                      |
| gr                   | git remote                                                                                                                       |
| gra                  | git remote add                                                                                                                   |
| grb                  | git rebase                                                                                                                       |
| grba                 | git rebase --abort                                                                                                               |
| grbc                 | git rebase --continue                                                                                                            |
| grbd                 | git rebase $(git_develop_branch)                                                                                                 |
| grbi                 | git rebase -i                                                                                                                    |
| grbm                 | git rebase $(git_main_branch)                                                                                                    |
| grbom                | git rebase origin/$(git_main_branch)                                                                                             |
| grbo                 | git rebase --onto                                                                                                                |
| grbs                 | git rebase --skip                                                                                                                |
| grev                 | git revert                                                                                                                       |
| grh                  | git reset                                                                                                                        |
| grhh                 | git reset --hard                                                                                                                 |
| groh                 | git reset origin/$(git_current_branch) --hard                                                                                    |
| grm                  | git rm                                                                                                                           |
| grmc                 | git rm --cached                                                                                                                  |
| grmv                 | git remote rename                                                                                                                |
| grrm                 | git remote remove                                                                                                                |
| grs                  | git restore                                                                                                                      |
| grset                | git remote set-url                                                                                                               |
| grss                 | git restore --source                                                                                                             |
| grst                 | git restore --staged                                                                                                             |
| grt                  | cd "$(git rev-parse --show-toplevel \|\| echo .)"                                                                                |
| gru                  | git reset --                                                                                                                     |
| grup                 | git remote update                                                                                                                |
| grv                  | git remote -v                                                                                                                    |
| gsb                  | git status -sb                                                                                                                   |
| gsd                  | git svn dcommit                                                                                                                  |
| gsh                  | git show                                                                                                                         |
| gsi                  | git submodule init                                                                                                               |
| gsps                 | git show --pretty=short --show-signature                                                                                         |
| gsr                  | git svn rebase                                                                                                                   |
| gss                  | git status -s                                                                                                                    |
| gst                  | git status                                                                                                                       |
| gsta                 | git stash push                                                                                                                   |
| gsta                 | git stash save                                                                                                                   |
| gstaa                | git stash apply                                                                                                                  |
| gstc                 | git stash clear                                                                                                                  |
| gstd                 | git stash drop                                                                                                                   |
| gstl                 | git stash list                                                                                                                   |
| gstp                 | git stash pop                                                                                                                    |
| gsts                 | git stash show --text                                                                                                            |
| gstu                 | git stash --include-untracked                                                                                                    |
| gstall               | git stash --all                                                                                                                  |
| gsu                  | git submodule update                                                                                                             |
| gsw                  | git switch                                                                                                                       |
| gswc                 | git switch -c                                                                                                                    |
| gswm                 | git switch $(git_main_branch)                                                                                                    |
| gswd                 | git switch $(git_develop_branch)                                                                                                 |
| gts                  | git tag -s                                                                                                                       |
| gtv                  | git tag \| sort -V                                                                                                               |
| gtl                  | gtl(){ git tag --sort=-v:refname -n -l ${1}* }; noglob gtl                                                                       |
| gunignore            | git update-index --no-assume-unchanged                                                                                           |
| gunwip               | git log -n 1 \| grep -q -c "\-\-wip\-\-" && git reset HEAD~1                                                                     |
| gup                  | git pull --rebase                                                                                                                |
| gupv                 | git pull --rebase -v                                                                                                             |
| gupa                 | git pull --rebase --autostash                                                                                                    |
| gupav                | git pull --rebase --autostash -v                                                                                                 |
| glum                 | git pull upstream $(git_main_branch)                                                                                             |
| gwch                 | git whatchanged -p --abbrev-commit --pretty=medium                                                                               |
| gwip                 | git add -A; git rm $(git ls-files --deleted) 2> /dev/null; git commit --no-verify --no-gpg-sign -m "--wip-- [skip ci]"           |
| gam                  | git am                                                                                                                           |
| gamc                 | git am --continue                                                                                                                |
| gams                 | git am --skip                                                                                                                    |
| gama                 | git am --abort                                                                                                                   |
| gamscp               | git am --show-current-patch                                                                                                      |

### Main branch preference

Following the recent push for removing racially-charged words from our technical vocabulary, the git plugin favors using
a branch name other than `master`. In this case, we favor the shorter, neutral and descriptive term `main`. This means
that any aliases and functions that previously used `master`, will use `main` if that branch exists. We do this via the
function `git_main_branch`.

### Deprecated aliases

These are aliases that have been removed, renamed, or otherwise modified in a way that may, or may not, receive further support.

| Alias  | Command                                                | Modification                                           |
| :----- | :----------------------------------------------------- | :----------------------------------------------------- |
| gap    | `git add --patch`                                      | new alias `gapa`                                       |
| gcl    | `git config --list`                                    | new alias `gcf`                                        |
| gdc    | `git diff --cached`                                    | new alias `gdca`                                       |
| gdt    | `git difftool`                                         | no replacement                                         |
| ggpull | `git pull origin $(current_branch)`                    | new alias `ggl` (`ggpull` still exists for now though) |
| ggpur  | `git pull --rebase origin $(current_branch)`           | new alias `ggu` (`ggpur` still exists for now though)  |
| ggpush | `git push origin $(current_branch)`                    | new alias `ggp` (`ggpush` still exists for now though) |
| gk     | `gitk --all --branches`                                | now aliased to `gitk --all --branches`                 |
| glg    | `git log --stat --max-count = 10`                      | now aliased to `git log --stat --color`                |
| glgg   | `git log --graph --max-count = 10`                     | now aliased to `git log --graph --color`               |
| gwc    | `git whatchanged -p --abbrev-commit --pretty = medium` | new alias `gwch`                                       |

## Functions

### Current

| Command                | Description                                                                                              |
|:-----------------------|:---------------------------------------------------------------------------------------------------------|
| `grename <old> <new>`  | Rename `old` branch to `new`, including in origin remote                                                 |
| current_branch         | Return the name of the current branch                                                                    |
| git_current_user_name  | Returns the `user.name` config value                                                                     |
| git_current_user_email | Returns the `user.email` config value                                                                    |
| git_main_branch        | Returns the name of the main branch: `main` if it exists, `master` otherwise                             |
| git_develop_branch     | Returns the name of the develop branch: `dev`, `devel`, `development` if they exist, `develop` otherwise |

### Work in Progress (WIP)

These features allow to pause a branch development and switch to another one (_"Work in Progress"_,  or wip). When you want to go back to work, just unwip it.

| Command          | Description                                     |
|:-----------------|:------------------------------------------------|
| work_in_progress | Echoes a warning if the current branch is a wip |
| gwip             | Commit wip branch                               |
| gunwip           | Uncommit wip branch                             |
