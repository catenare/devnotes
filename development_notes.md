# Front End development
## Serve local file
* Browser-sync Command - *browser-sync start --server --directory --files "**/*"*
## Requirejs
* For r.js to work (without explicit path).
  * *npm install -g requirejs*

# Using Browser-sync
## Browser-sync Command - `browser-sync start --server --directory --files "**/*"`

## Git
* Allow unrelated histories [StackOverflow](http://stackoverflow.com/questions/37937984/git-refusing-to-merge-unrelated-histories)
  * ```git pull remote branch --allow-unrelated-histories```

* Remove file from git repository without deleting local file. [StackOverflow](http://stackoverflow.com/questions/1143796/remove-a-file-from-a-git-repository-without-deleting-it-from-the-local-filesyste)
  * ```git rm --cached myfile.fil``` or ```git rm --cached -r myfile```
