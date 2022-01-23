---
title: Dotfiles
updated: 2021-07-25 09:35:12Z
created: 2021-07-25 09:21:16Z
latitude: -26.16670000
longitude: 27.86670000
altitude: 0.0000
---

## Resources
* http://dotfiles.github.io/faq/
* https://github.com/webpro/awesome-dotfiles
* https://www.atlassian.com/git/tutorials/dotfiles
### Moving to using dotfiles for managing resources

- [Manage dotfiles with git](https://medium.com/toutsbrasil/how-to-manage-your-dotfiles-with-git-f7aeed8adf8b)

```
git init --bare $HOME/.dotfiles
alias dotfiles='/usr/bin/git --git-dir=$HOME/.dotfiles/ --work-tree=$HOME'
dotfiles config --local status.showUntrackedFiles no
dotfiles remote add origin git@personal:catenare/dotfiles.git
```