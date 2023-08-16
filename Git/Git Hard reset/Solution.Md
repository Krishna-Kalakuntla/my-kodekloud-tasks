he Nautilus application development team was working on a git repository /usr/src/kodekloudrepos/beta present on Storage server in Stratos DC. This was just a test repository and one of the developers just pushed a couple of changes for testing, but now they want to clean this repository along with the commit history/work tree, so they want to point back the HEAD and the branch itself to a commit with message add data.txt file. Find below more details:

In /usr/src/kodekloudrepos/beta git repository, reset the git commit history so that there are only two commits in the commit history i.e initial commit and add data.txt file.

Also make sure to push your changes.

```
cd /usr/src/kodekloudrepos/beta/
git status
git log
git reset --hard 74febcf60ad33d30f9666458487fa92c06632108
git push --force  origin master

```