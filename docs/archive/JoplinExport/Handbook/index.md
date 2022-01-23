---
title: index
updated: 2021-07-03 10:42:56Z
created: 2020-09-10 23:53:43Z
---

# Developer Notes

!!! notes
Using Mkdocs to track my daily developer activities. These are things that I'm doing and not necessarily code snippets although I will put snippets of code here. It is to track what I'm working on and what I'm doing.
Notes are stored on bitbucket in a privte repository.
Private notes and information that shouldn't be public gets added to OneNote or to 1Password depending on how sensitive it is.
This is not a public repository.
[Notes](../Handbook/Notes.md)

## Local setup (Johan's machine)

- **/etc/hosts** file. 
  * Added `127.0.0.1 db` to access docker database connection.
  * Added `127.0.0.1 redis-server` to access docker redis server.
- Scripts for local setup repo: [Github Repo](https://github.com/johanmnext45/snippets) - Private repo

## Resources

- [Docfox Wiki](https://github.com/docfoxapp/docfox-rework/wiki)

## App and commandline shortcuts

### [MassCode](https://masscode.io) - Snippet manager

- Adding a snippet: ++cmd+n++
- Copying a snippet: ++shift+cmd+c++
- Formatting as snippet: ++shift+cmd+f++
- Fragment: ++cmd+t++
- Show Assistant: ++option+s++

### [FlyCut](https://github.com/TermiT/Flycut)

- HotKey: ++shift+command+v++

### Visual Studio Code

- [Keyboard Shortcuts](https://code.visualstudio.com/shortcuts/keyboard-shortcuts-macos.pdf)

* Multiple Cursors:

  - Insert Cursor: ++option++ click
  - Next line: ++option+command++ down_arrow

### [Macports](https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/macports)

| Alias | Command                           | Description                                                  |
| ----- | --------------------------------- | ------------------------------------------------------------ |
| pc    | `sudo port clean --all installed` | Clean up intermediate installation files for installed ports |
| pi    | `sudo port install`               | Install package given as argument                            |
| psu   | `sudo port selfupdate`            | Update ports tree with MacPorts repository                   |
| puni  | `sudo port uninstall inactive`    | Uninstall inactive ports                                     |
| puo   | `sudo port upgrade outdated`      | Upgrade ports with newer versions available                  |
| pup   | `psu && puo`                      | Update ports tree, then upgrade ports to newest versions     |

### Ruby

| Alias | Command                                | Description                                          |
| ----- | -------------------------------------- | ---------------------------------------------------- |
| rb    | `ruby`                                 | The Ruby command                                     |
| sgem  | `sudo gem`                             | Run sudo gem on the system ruby, not the active ruby |
| rfind | `find . -name "*.rb" \| xargs grep -n` | Find ruby file                                       |
| gin   | `gem install`                          | Install a gem into the local repository              |
| gun   | `gem uninstall`                        | Uninstall gems from the local repository             |
| gli   | `gem list`                             | Display gems installed locally                       |

#### Rails aliases

| Alias  | Command                    | Description                                        |
| ------ | -------------------------- | -------------------------------------------------- |
| `rc`   | `rails console`            | Interact with your Rails app from the CLI          |
| `rcs`  | `rails console --sandbox`  | Test code in a sandbox, without changing any data  |
| `rd`   | `rails destroy`            | Undo a generate operation                          |
| `rdb`  | `rails dbconsole`          | Interact with your db from the console             |
| `rgen` | `rails generate`           | Generate boilerplate code                          |
| `rgm`  | `rails generate migration` | Generate a db migration                            |
| `rp`   | `rails plugin`             | Run a Rails plugin command                         |
| `ru`   | `rails runner`             | Run Ruby code in the context of Rails              |
| `rs`   | `rails server`             | Launch a web server                                |
| `rsd`  | `rails server --debugger`  | Launch a web server with debugger                  |
| `rsp`  | `rails server --port`      | Launch a web server and specify the listening port |

##### Rake aliases

| Alias   | Command                         | Description                                            |
| ------- | ------------------------------- | ------------------------------------------------------ |
| `rdm`   | `rake db:migrate`               | Run pending db migrations                              |
| `rdms`  | `rake db:migrate:status`        | Show current db migration status                       |
| `rdmtc` | `rake db:migrate db:test:clone` | Run pending migrations and clone db into test database |
| `rdr`   | `rake db:rollback`              | Roll back the last migration                           |
| `rdc`   | `rake db:create`                | Create the database                                    |
| `rds`   | `rake db:seed`                  | Seed the database                                      |
| `rdd`   | `rake db:drop`                  | Delete the database                                    |
| `rdrs`  | `rake db:reset`                 | Delete the database and set it up again                |
| `rdtc`  | `rake db:test:clone`            | Clone the database into the test database              |
| `rdtp`  | `rake db:test:prepare`          | Duplicate the db schema into your test database        |
| `rdsl`  | `rake db:schema:load`           | Load the database schema                               |
| `rlc`   | `rake log:clear`                | Clear Rails logs                                       |
| `rn`    | `rake notes`                    | Search for notes (`FIXME`, `TODO`) in code comments    |
| `rr`    | `rake routes`                   | List all defined routes                                |
| `rrg`   | `rake routes \| grep`           | List and filter the defined routes                     |
| `rt`    | `rake test`                     | Run Rails tests                                        |
| `rmd`   | `rake middleware`               | Interact with Rails middlewares                        |
| `rsts`  | `rake stats`                    | Print code statistics                                  |

##### Utility aliases

| Alias     | Command                       | Description                                    |
| --------- | ----------------------------- | ---------------------------------------------- |
| `devlog`  | `tail -f log/development.log` | Show and follow changes to the development log |
| `prodlog` | `tail -f log/production.log`  | Show and follow changes to the production log  |
| `testlog` | `tail -f log/test.log`        | Show and follow changes to the test log        |

##### Environment settings

| Alias | Command                 | Description                     |
| ----- | ----------------------- | ------------------------------- |
| `RED` | `RAILS_ENV=development` | Sets `RAILS_ENV` to development |
| `REP` | `RAILS_ENV=production`  | Sets `RAILS_ENV` to production  |
| `RET` | `RAILS_ENV=test`        | Sets `RAILS_ENV` to test        |

These are global aliases. Use in combination with a command or just run them
separately. For example: `REP rake db:migrate` will migrate the production db.

### Tmux

- [CheatSheet](https://tmuxcheatsheet.com/)

* ++ctrl+b++ " - Split window vertical

- ++ctrl+b++ % - Split window horizontal

| Alias  | Command                | Description                                              |
| ------ | ---------------------- | -------------------------------------------------------- |
| `ta`   | tmux attach -t         | Attach new tmux session to already running named session |
| `tad`  | tmux attach -d -t      | Detach named tmux session                                |
| `ts`   | tmux new-session -s    | Create a new named tmux session                          |
| `tl`   | tmux list-sessions     | Displays a list of running tmux sessions                 |
| `tksv` | tmux kill-server       | Terminate all running tmux sessions                      |
| `tkss` | tmux kill-session -t   | Terminate named running tmux session                     |
| `tmux` | `_zsh_tmux_plugin_run` | Start a new tmux session                                 |

#### Configuration Variables

| Variable                            | Description                                                                   |
| ----------------------------------- | ----------------------------------------------------------------------------- |
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

### NeoVim(Vim)

- Some commands
- `:e filename` - can use tab to search files
- `:buffers` - List open buffers
- `:b1` - go to buffer number

### Git

- Ignore files specific to docfox `git config --local core.excludesFile ~/projects/bin/resources/.docfox_gitignore`

- Ignore a file already checked in. `git rm --cached _file_`
- User their commit. `git merge --strategy-option theirs`

#### Github client

- Github Command Line Client

  - Create a pr: `gh pr create --title "Pull request title" --body "Pull request body"`

  * [Github Client](https://github.com/cli/cli)
  * [Github CLI Manual](https://cli.github.com/manual/)

  ## Notes

  - Potential tool to track outgoing connections: [Lulu](https://objective-see.com/products/lulu.html)


## Developer Notebook for Johan Martin
![Notebook](https://openclipart.org/download/100339/notebook-black.svg")
Snippets and solutions to issues I have encountered.

### My Info
* Contact me for web development projects
* Phone: (646) 783-9811 or +27 81 443 8234
* [martin.johan@johan-martin.com](mailto:martin.johan@johan-martin.com)

### My Links
* [www.johan-martin.com](https://www.johan-martin.com)
* [Git Projects](https://github.com/catenare)

### Recommendations
* I think this is the best paper notebook for developers. Confidant available from [Baron Fig](https://www.baronfig.com/) 
![Baron Fig](https://cdn.shopify.com/s/files/1/0543/1257/products/confidant_charcoal_flagship_01.jpg?v=1489606782)

