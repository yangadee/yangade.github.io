---
layout: page
title: "PAGE TITLE"
permalink: /hi/test/.md
---

## Merge two remote branches
If you have remote-tracking branches set up locally, it's as simple as:
```
git checkout master
git merge slave
git push origin master
``` 
If you have not yet set up remote-tracking branches, you could do something like:
```
git fetch origin
git checkout master     # or `git checkout -b production origin/production` if you haven't set up production branch locally
git merge origin/slave
git push origin master
```
Exceptions:
if you get the exception below while using `merge`
```
refusing to merge unrelated histories
```
Solution:
```
git merge development --allow-unrelated-histories
```
## To delete a remote branch:
```
git push origin :<remoted branch>
```
## To delete a local branch:
```
git branch -d <branch name>
```
## config **git**
``` bat
git config --global core.editor vim     #To config `vim` as default editor for git
Git congfig –global user.email “<>”
Git config –globlal user.name “<>”
Git congfig –global alias.ck checkout   #change alias of checkout into ck
```
## References
* [https://zlargon.gitbooks.io/git-tutorial/content/](https://zlargon.gitbooks.io/git-tutorial/content/)
