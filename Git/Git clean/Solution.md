The Nautilus application development team was working on a git repository /usr/src/kodekloudrepos/official present on Storage server in Stratos DC. One of the developers mistakenly created a couple of files under this repository, but now they want to clean this repository without adding/pushing any new files. Find below more details:

Clean the /usr/src/kodekloudrepos/official git repository without adding/pushing any new files, make sure git status is clean.

```
ssh natasha@ststor01

cd /usr/src/kodekloudrepos/official

git clean

git status
```