The Nautilus application development team was working on a git repository /usr/src/kodekloudrepos/media present on Storage server in Stratos DC. One of the developers stashed some in-progress changes in this repository, but now they want to restore some of the stashed changes. Find below more details to accomplish this task:
Look for the stashed changes under /usr/src/kodekloudrepos/media git repository, and restore the stash with stash@{1} identifier. Further, commit and push your changes to the origin.

```
cd /usr/src/kodekloudrepos/media/
git status
git stash  list
git stash pop stash@{1}
git add .
git commit -m "Added welcome.txt file"
git push origin master
```