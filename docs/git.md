# Git notes
## Using git for version control. Lessons learned.

### Git error message. Can't merge unrelated histories.
* Allow unrelated histories [StackOverflow Issue](http://stackoverflow.com/questions/37937984/git-refusing-to-merge-unrelated-histories)
  * git pull remote branch --allow-unrelated-histories

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

### Github Markdown
* Languages for code blocks - [highlights.js](https://highlightjs.org/static/demo/)
* Emoji List - :bowtie [Emoji Cheat Sheet](http://www.webpagefx.com/tools/emoji-cheat-sheet/)