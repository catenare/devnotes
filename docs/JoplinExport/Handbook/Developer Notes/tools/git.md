---
title: git
updated: 2021-05-19 09:42:36Z
created: 2020-09-10 22:07:13Z
---

# Git notes
## Using git for version control. Lessons learned.

## How To
* **Git tag**
    1. Adding a tag
        * `git tag v1.0`
        * `git push origin --tags` - push to github
    1. Deleting tags
        * `git tag -d v1.0`
        * `git push origin :refs/tags/v1.0`
    1. Get all tags including remote tags
        * `git fetch --all --tags --prune` - get all remote tags and remove repos removed by remote.
	1. Remove from remotes locally ignored files and folders
		* `git rm -r --cached some-directory`
    * Need tags for composer
* **git worktree** [Git Worktree](https://git-scm.com/docs/git-worktree)
    * Create temporary checkout for working on a branch without having to stash data
* Delete local and remote branches
```bash
git push -d <remote_name> <branch_name>
git branch -d <branch_name>
```
* Update local list and prune branches
    * `git fetch -p` -p is for prunining

### Git Resources
* Styleguide for git messages - [Udacity Git Styleguide](https://udacity.github.io/git-styleguide/)
#### .gitignore
* Resources
  * [.gitignore templates](https://github.com/github/gitignore)
    * Collection of .gitignore templates
  * [gitignore.io](https://www.gitignore.io/)
* Global .gitignore [Stackoverflow 7335420](http://stackoverflow.com/questions/7335420/global-git-ignore)
  * `~/.config/git/ignore` - default location
  * `git config --global core.excludesfile '~/.gitignore'` - set the location

### Git error message. Can't merge unrelated histories.
* Allow unrelated histories [StackOverflow Issue](http://stackoverflow.com/questions/37937984/git-refusing-to-merge-unrelated-histories)
  * `git pull remote branch --allow-unrelated-histories`

### Git error trying to push when pull seems to work

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

### Removing sensitive data from git after having committed [Removing Sensitive Data - Github]( https://help.github.com/articles/removing-sensitive-data-from-a-repository/)

* ```git filter-branch --force --index-filter 'git rm --cached --ignore-unmatch {path/filename}' --prune-empty --tag-name-filter cat -- --all```
* ```git push github --force --all```
* Remove the references
  * ```git for-each-ref --format='delete %(refname)' refs/original | git update-ref --stdin```
  * ```git reflog expire --expire=now --all```
  * ```git gc --prune=now```

* No guarantee that the data hasn't been downloaded or forked but at least it's removed going forward.

### Git create empty branch
* [Create Orphan Branch](http://www.bitflop.dk/tutorials/how-to-create-a-new-and-empty-branch-in-git.html)
* Steps:
    1. `git checkout --orphan NEWBRANCH`
    1. `git rm -rf .`
    1. `git remote add {name} {git remote branch}`
    1. `git pull -u {name} {branch}`
    1. `git push -u {name} {branch}`
* Now one have a copy of another branch in working branch.

### Github Markdown
* Languages for code blocks - [highlights.js](https://highlightjs.org/static/demo/)
* Emoji List - :bowtie [Emoji Cheat Sheet](http://www.webpagefx.com/tools/emoji-cheat-sheet/)
### Remote branches not showing on local. Only shows *master*.
* `git branch -a` show all branches
* `git checkout --track remote/branch` - pulls in the remote branch.

### Unrelated histories
* `git pull --allow-unrelated-histories`
