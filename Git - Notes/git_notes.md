# ** Complete Git Notes **
---

## Configure Git 

**Setting Username and Email for Git:**

`git config --global user.name "Your Name"`

`git config --global user.email "your.email@your-place.com"`

**Git Integration:**

`git config --global core.editor "subl -n -w"`

**Configure P4Merge as Diff Tool in Git:**
[Download p4merge for MAC](https://www.perforce.com/products/helix-core-apps/merge-diff-tool-p4merge)

`git config --global diff.tool p4merge`

`git config --global difftool.p4merge.path "/Applications/p4merge.app/Contents/MacOS/p4merge"`

`git config --global difftool.prompt false`

**Configure P4Merge as Merge Tool in Git:**

`git config --global merge.tool p4merge`

`git config --global mergetool.p4merge.path "/Applications/p4merge.app/Contents/MacOS/p4merge"`

`git config --global mergetool.prompt false`

**View Git Config:**

`git config --global -e`

---

## The Basics
**Initialize git:**

`git init`

**Three stages in Git:**

Working directory - Staging Directory - Repository

**Common commands**

`git status    #checks the status`

`git add       #adds the file to staging dir`

`git commit    #Commits the files added ## Add -m For adding messageswhile commiting.`

**Check git Log with:**

`git log`

_Sample out:_
```
m-C02SMGEMG8WN:demo s0m01cp$ git log
commit 38ee2011bd5a97e0ff6e7958bfe7ecaefcf63602
Author: s0m01cp <s0m01cp@m-C02SMGEMG8WN.local>
Date:   Tue Feb 27 14:59:41 2018 +0530

    Adding both README
    and a LICENSE file

commit 793657cc15dedda8489bce2f665795cbe28be653
Author: s0m01cp <s0m01cp@m-C02SMGEMG8WN.local>
Date:   Tue Feb 27 14:54:26 2018 +0530

    First commit
m-C02SMGEMG8WN:demo s0m01cp$
```
**The Show Command**

`git show [options] <object>`

`git show [options]`

_Sample out:_
```
m-C02SMGEMG8WN:demo s0m01cp$ git show
commit 38ee2011bd5a97e0ff6e7958bfe7ecaefcf63602
Author: s0m01cp <s0m01cp@m-C02SMGEMG8WN.local>
Date:   Tue Feb 27 14:59:41 2018 +0530

    Adding both README
    and a LICENSE file

diff --git a/LICENSE.md b/LICENSE.md
new file mode 100644
index 0000000..86c249f
--- /dev/null
+++ b/LICENSE.md
@@ -0,0 +1,3 @@
+#License
+
+##Sample V 2.0
m-C02SMGEMG8WN:demo s0m01cp$
```
**List Files being tracked by Git**

`git ls-files `

**Adding and Commiting with messges**

`git commit -am`

**Backing out Changes/Reaverting a Commit**

_To unstage a change in the staging area_

`git reset HEAD README.md`

**Discard the changes made and go back to the previous version of the file on Git**

`git checkout -- README.md`

_Sample Snippet_

```
m-C02SMGEMG8WN:demo s0m01cp$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")

m-C02SMGEMG8WN:demo s0m01cp$ git add .

m-C02SMGEMG8WN:demo s0m01cp$ ls -lrth
total 16
-rw-r--r--  1 s0m01cp  HOMEOFFICE\Domain Users    25B Feb 27 14:59 LICENSE.md
-rw-r--r--  1 s0m01cp  HOMEOFFICE\Domain Users    90B Feb 27 15:24 README.md

m-C02SMGEMG8WN:demo s0m01cp$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   README.md


m-C02SMGEMG8WN:demo s0m01cp$ git reset HEAD README.md
Unstaged changes after reset:
M	README.md

m-C02SMGEMG8WN:demo s0m01cp$ git checkout -- README.md

m-C02SMGEMG8WN:demo s0m01cp$ git status
On branch master
nothing to commit, working tree clean

```

**Best Command for git history**
`git log --oneline --graph --decorate --all`

**Create an alias for the above or any**

`git config --global alias.hist "log --oneline --graph --decorate --all"`

_Test the history alias with_

`git hist`

_history on the readme.md file_

`git hist -- README.md`

**List all the config Vars set:**

`git config --global --list`

**Renaming a file that is being tracked by git**

`git mv example.txt demo.txt`

`git status`

`git commit -m "renaming example"`

**Remove a file that is being tracked by git:**

`git rm demo.txt`

**Managing files outside git (untracked files) - To add changes that are made on OS level**
for updating any deletion or any action of that sort (-u for update)

`git add -u`  

In orger to incluse both additions and deleteions use below

`git add -A`

**Excluding Unwanted files**
Add the patterns or files nder the below file to exclude any files or folders to be tracked in git. 

`.gitignore`

_Sample Example_

```
m-C02SMGEMG8WN:demo s0m01cp$ ls -lrth
total 16
-rw-r--r--  1 s0m01cp  74715970    25B Feb 27 14:59 LICENSE.md
-rw-r--r--  1 s0m01cp  74715970    60B Feb 27 15:25 README.md
-rw-r--r--  1 s0m01cp  74715970     0B Mar  3 09:11 application.log
m-C02SMGEMG8WN:demo s0m01cp$ cat .gitignore
*.log
m-C02SMGEMG8WN:demo s0m01cp$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	.gitignore

nothing added to commit but untracked files present (use "git add" to track)
m-C02SMGEMG8WN:demo s0m01cp$ git add .gitignore
m-C02SMGEMG8WN:demo s0m01cp$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   .gitignore

m-C02SMGEMG8WN:demo s0m01cp$ git commit -m "Added gitignore files"
[master e598d0f] Added gitignore files
 1 file changed, 1 insertion(+)
 create mode 100644 .gitignore
m-C02SMGEMG8WN:demo s0m01cp$ git status
On branch master
nothing to commit, working tree clean
```
---
## Advanced: Beyond the Basics
**Comparing Differences**

Below shows what was reecntly changed in the working directory with the HEAD in the repositry. 

`git diff` 

`git difftool`

Comparing different commits and different levels

`git hist`

`git diff 38ee201 HEAD`

`git diff branch1 master`   # diff can work with branches too 

_HEAD signifies for the latest commit in git currently_

```
m-C02SMGEMG8WN:demo s0m01cp$ git hist
* e598d0f (HEAD -> master) Added gitignore files
* 164c389 Deleting demo
* a391e52 rename example
* d9e6190 ading an example file
* 24df27c Updating README
* 38ee201 Adding both README and a LICENSE file
* 793657c First commit
m-C02SMGEMG8WN:demo s0m01cp$ git diff 38ee201 HEAD
diff --git a/.gitignore b/.gitignore
new file mode 100644
index 0000000..397b4a7
--- /dev/null
+++ b/.gitignore
@@ -0,0 +1 @@
+*.log
diff --git a/README.md b/README.md
index 76732c1..02e9f0a 100644
--- a/README.md
+++ b/README.md
@@ -1,4 +1,5 @@
 #Demo Project Readme

 This is a sample read me.
-
+
+some text
m-C02SMGEMG8WN:demo s0m01cp$
```

**Open configured difftool for comparing:**

`git difftool 38ee201 HEAD`

**Branching and Merging**

Branch = Timeline of commits
Branch Names are Labels, Deletion removes lables only.

[Git - Basic Branching and Merging](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)

**Special Markers in GIT (Pointers)**

HEAD
- Points to last commit of current branch
- can be moved (check advanced)

**Branching**

`git branch`

`git checkout -b <name of the branch>`

`git diff branch1 master`

To point to your master branch

`git checkout master`

Sample: 

```
m-C02SMGEMG8WN:demo s0m01cp$ git branch
* master
m-C02SMGEMG8WN:demo s0m01cp$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
m-C02SMGEMG8WN:demo s0m01cp$ git checkout -b updates
M	README.md
Switched to a new branch 'updates'

m-C02SMGEMG8WN:demo s0m01cp$ vi README.md

m-C02SMGEMG8WN:demo s0m01cp$ git add .

m-C02SMGEMG8WN:demo s0m01cp$ #git commit -m "Adding updates from branch"

m-C02SMGEMG8WN:demo s0m01cp$ git status
On branch updates
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   README.md

m-C02SMGEMG8WN:demo s0m01cp$ #git commit -m "Adding updates from branch"

m-C02SMGEMG8WN:demo s0m01cp$ git commit -m "Adding updates from branch"
[updates c77decd] Adding updates from branch
 1 file changed, 3 insertions(+), 1 deletion(-)
 
m-C02SMGEMG8WN:demo s0m01cp$ git hist
* c77decd (HEAD -> updates) Adding updates from branch
* e598d0f (master) Added gitignore files
* 164c389 Deleting demo
* a391e52 rename example
* d9e6190 ading an example file
* 24df27c Updating README
* 38ee201 Adding both README and a LICENSE file
* 793657c First commit

m-C02SMGEMG8WN:demo s0m01cp$ git diff updates master
diff --git a/README.md b/README.md
index 996d4c2..02e9f0a 100644
--- a/README.md
+++ b/README.md
@@ -2,6 +2,4 @@

 This is a sample read me.

-some text
-
-just some update,some more updates
+some text

m-C02SMGEMG8WN:demo s0m01cp$ git branch
  master
* updates

m-C02SMGEMG8WN:demo s0m01cp$ git checkout master
Switched to branch 'master'

m-C02SMGEMG8WN:demo s0m01cp$ git hist
* c77decd (updates) Adding updates from branch
* e598d0f (HEAD -> master) Added gitignore files
* 164c389 Deleting demo
* a391e52 rename example
* d9e6190 ading an example file
* 24df27c Updating README
* 38ee201 Adding both README and a LICENSE file
* 793657c First commit
m-C02SMGEMG8WN:demo s0m01cp$
```

**Deleting a branch**

`git branch -d <Branch Name>`

Sample 
```
m-C02SMGEMG8WN:demo s0m01cp$ git branch -d updates
Deleted branch updates (was c77decd).
m-C02SMGEMG8WN:demo s0m01cp$
```

**Merging**

`git merge <branch name>`

To open in merge tool

`git mergetool`

sample for fast forward branch: 

```
m-C02SMGEMG8WN:demo s0m01cp$ git hist
* c77decd (updates) Adding updates from branch
* e598d0f (HEAD -> master) Added gitignore files
* 164c389 Deleting demo
* a391e52 rename example
* d9e6190 ading an example file
* 24df27c Updating README
* 38ee201 Adding both README and a LICENSE file
* 793657c First commit
m-C02SMGEMG8WN:demo s0m01cp$ git merge updates
Updating e598d0f..c77decd
Fast-forward
 README.md | 4 +++-
 1 file changed, 3 insertions(+), 1 deletion(-)
m-C02SMGEMG8WN:demo s0m01cp$ git hist
* c77decd (HEAD -> master, updates) Adding updates from branch
* e598d0f Added gitignore files
* 164c389 Deleting demo
* a391e52 rename example
* d9e6190 ading an example file
* 24df27c Updating README
* 38ee201 Adding both README and a LICENSE file
* 793657c First commit
```

**Tags**

**_Lightweight tag_**

`git tag <tag name>`

To list all tags

`git tag --list`

To delete a tag 

`git tag -d <tag name>`

**_Annotated tag_**

Annotating tag with version number and committing the tag 

`git tag -a v1.0 -m "Release 1.0"`

`git tag --list`

Sample

```
m-C02SMGEMG8WN:demo s0m01cp$ git hist
* fc6066e (HEAD -> master) trouble 1
*   cbc3e04 Merge branch 'very-bad'
|\
| * 4de0a33 (very-bad) Very bad update
* | 7d4b737 Causing issues again
|/
* c77decd Adding updates from branch
* e598d0f Added gitignore files
* 164c389 Deleting demo
* a391e52 rename example
* d9e6190 ading an example file
* 24df27c Updating README
* 38ee201 Adding both README and a LICENSE file
* 793657c First commit
m-C02SMGEMG8WN:demo s0m01cp$ git tag -a v1.0 -m "Release 1.0"
m-C02SMGEMG8WN:demo s0m01cp$ git tag --list
v1.0
m-C02SMGEMG8WN:demo s0m01cp$ git hist
* fc6066e (HEAD -> master, tag: v1.0) trouble 1
*   cbc3e04 Merge branch 'very-bad'
|\
| * 4de0a33 (very-bad) Very bad update
* | 7d4b737 Causing issues again
|/
* c77decd Adding updates from branch
* e598d0f Added gitignore files
* 164c389 Deleting demo
* a391e52 rename example
* d9e6190 ading an example file
* 24df27c Updating README
* 38ee201 Adding both README and a LICENSE file
* 793657c First commit
m-C02SMGEMG8WN:demo s0m01cp$
```

All info with tag:

`git show <tagname>`

Sample

`git show v1.0`

```
m-C02SMGEMG8WN:demo s0m01cp$ git show v1.0
tag v1.0
Tagger: s0m01cp <s0m01cp@m-C02SMGEMG8WN.local>
Date:   Sat Mar 3 15:23:42 2018 +0530

Release 1.0

commit fc6066e61699c63229ba389ed5c4b55b5054b93e
Author: s0m01cp <s0m01cp@m-C02SMGEMG8WN.local>
Date:   Sat Mar 3 15:15:06 2018 +0530

    trouble 1

diff --git a/README.md b/README.md
index 581e1ab..c6abbe3 100644
--- a/README.md
+++ b/README.md
@@ -4,4 +4,4 @@ This is a sample read me.

 some text

-This is trouble
+This is trouble and is it ok. This is not ok.
m-C02SMGEMG8WN:demo s0m01cp$
```

**Work in progress and stashing**

`git stash` at any point to stach save the changes you want to get back to. 

`git stash list` lists all the stash currently available. 

git status at this point shows clean results. 

Edit the changes required and git commit them and run 

`git stash pop`  this pushes the unsaved commit from previous stash list and drops it from stash list. 

```
m-C02SMGEMG8WN:demo s0m01cp$ git checkout master
Switched to branch 'master'
m-C02SMGEMG8WN:demo s0m01cp$ open README.md
m-C02SMGEMG8WN:demo s0m01cp$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
m-C02SMGEMG8WN:demo s0m01cp$ git stash
Saved working directory and index state WIP on master: fc6066e trouble 1
HEAD is now at fc6066e trouble 1
m-C02SMGEMG8WN:demo s0m01cp$ git stash list
stash@{0}: WIP on master: fc6066e trouble 1
m-C02SMGEMG8WN:demo s0m01cp$ git status
On branch master
nothing to commit, working tree clean

m-C02SMGEMG8WN:demo s0m01cp$ open LICENSE.md

m-C02SMGEMG8WN:demo s0m01cp$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   LICENSE.md

no changes added to commit (use "git add" and/or "git commit -a")
m-C02SMGEMG8WN:demo s0m01cp$ git commit -am "updating licence first "
[master 7a1a7f0] updating licence first
 1 file changed, 1 insertion(+)
 
m-C02SMGEMG8WN:demo s0m01cp$ git status
On branch master
nothing to commit, working tree clean

m-C02SMGEMG8WN:demo s0m01cp$ git stash pop
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
Dropped refs/stash@{0} (d7b2415db731e8d09bea54ad02abee1367bce307)
m-C02SMGEMG8WN:demo s0m01cp$ git commit -am "updating readme"
[master 4180ee4] updating readme
 1 file changed, 2 insertions(+)
m-C02SMGEMG8WN:demo s0m01cp$ git status
On branch master
nothing to commit, working tree clean
m-C02SMGEMG8WN:demo s0m01cp$ git stash list
m-C02SMGEMG8WN:demo s0m01cp$
```

**Time travel with reset and reflog**
- soft reset

  `git reset <commit code> --soft`

Pointes Head to the mentioned commit code. This preserves our staging area and working directory changes. 

Sample: 
```
m-C02SMGEMG8WN:demo s0m01cp$ git hist
* 4180ee4 (HEAD -> master) updating readme
* 7a1a7f0 updating licence first
* fc6066e (tag: v1.0, very-bad) trouble 1
*   cbc3e04 Merge branch 'very-bad'
|\
| * 4de0a33 Very bad update
* | 7d4b737 Causing issues again
|/
* c77decd Adding updates from branch
* e598d0f Added gitignore files
* 164c389 Deleting demo
* a391e52 rename example
* d9e6190 ading an example file
* 24df27c Updating README
* 38ee201 Adding both README and a LICENSE file
* 793657c First commit
m-C02SMGEMG8WN:demo s0m01cp$ git reset fc6066e --soft
m-C02SMGEMG8WN:demo s0m01cp$ git hist
* fc6066e (HEAD -> master, tag: v1.0, very-bad) trouble 1
*   cbc3e04 Merge branch 'very-bad'
|\
| * 4de0a33 Very bad update
* | 7d4b737 Causing issues again
|/
* c77decd Adding updates from branch
* e598d0f Added gitignore files
* 164c389 Deleting demo
* a391e52 rename example
* d9e6190 ading an example file
* 24df27c Updating README
* 38ee201 Adding both README and a LICENSE file
* 793657c First commit
m-C02SMGEMG8WN:demo s0m01cp$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   LICENSE.md
	modified:   README.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   README.md

```

- mixed rest 

  `git reset <commit code> --mixed`
  
files gets unstaged in our working directory. There will be nothing in out staging area. 

```
m-C02SMGEMG8WN:demo s0m01cp$ git reset c77decd -- mixed
Unstaged changes after reset:
M	LICENSE.md
M	README.md
m-C02SMGEMG8WN:demo s0m01cp$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   LICENSE.md
	modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```

- hard reset

  `git reset <commit code> --hard`
  
Any changes that have been pending will be wiped out. (Most destructive)

```
m-C02SMGEMG8WN:demo s0m01cp$ git reset 24df27c --hard
HEAD is now at 24df27c Updating README
m-C02SMGEMG8WN:demo s0m01cp$ git status
On branch master
nothing to commit, working tree clean
m-C02SMGEMG8WN:demo s0m01cp$ git hist
* fc6066e (tag: v1.0, very-bad) trouble 1
*   cbc3e04 Merge branch 'very-bad'
|\
| * 4de0a33 Very bad update
* | 7d4b737 Causing issues again
|/
* c77decd Adding updates from branch
* e598d0f Added gitignore files
* 164c389 Deleting demo
* a391e52 rename example
* d9e6190 ading an example file
* 24df27c (HEAD -> master) Updating README
* 38ee201 Adding both README and a LICENSE file
* 793657c First commit
m-C02SMGEMG8WN:demo s0m01cp$ git log --oneline
24df27c Updating README
38ee201 Adding both README and a LICENSE file
793657c First commit
```
**Reflog**
This indicates our logs in a referenced way (Commits, resets and merges)

`git reflog`

Sample:
```
m-C02SMGEMG8WN:demo s0m01cp$ git reflog
24df27c HEAD@{0}: reset: moving to 24df27c
c77decd HEAD@{1}: reset: moving to c77decd
fc6066e HEAD@{2}: reset: moving to fc6066e
4180ee4 HEAD@{3}: commit: updating readme
7a1a7f0 HEAD@{4}: reset: moving to HEAD
7a1a7f0 HEAD@{5}: commit: updating licence first
fc6066e HEAD@{6}: reset: moving to HEAD
fc6066e HEAD@{7}: checkout: moving from very-bad to master
fc6066e HEAD@{8}: merge master: Fast-forward
4de0a33 HEAD@{9}: checkout: moving from master to very-bad
fc6066e HEAD@{10}: checkout: moving from very-bad to master
4de0a33 HEAD@{11}: checkout: moving from master to very-bad
fc6066e HEAD@{12}: commit: trouble 1
cbc3e04 HEAD@{13}: checkout: moving from very-bad to master
4de0a33 HEAD@{14}: checkout: moving from master to very-bad
cbc3e04 HEAD@{15}: merge very-bad: Merge made by the 'recursive' strategy.
7d4b737 HEAD@{16}: commit: Causing issues again
c77decd HEAD@{17}: checkout: moving from very-bad to master
4de0a33 HEAD@{18}: commit: Very bad update
c77decd HEAD@{19}: checkout: moving from master to very-bad
c77decd HEAD@{20}: merge updates: Fast-forward
e598d0f HEAD@{21}: checkout: moving from updates to master
c77decd HEAD@{22}: commit: Adding updates from branch
e598d0f HEAD@{23}: checkout: moving from master to updates
e598d0f HEAD@{24}: commit: Added gitignore files
164c389 HEAD@{25}: commit: Deleting demo
a391e52 HEAD@{26}: commit: rename example
d9e6190 HEAD@{27}: commit: ading an example file
24df27c HEAD@{28}: commit: Updating README
```
---
## GitHub Remote:

_shows all remote links in github repository_

`git remote -v`

_Add a remote link to git._

`git remote add origin https://github.com/i5uhail/demo.git`

**GitHub Push Commands**

-u or --set-upstream is required only for the inital push

`git push -u origin master --tags`

`git push origin master --tags`

---

## Authentication: 

**Generating an SSH Key**

`cd <homedir>/.ssh`

`ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`

---
## Git Cloning (More about Git): 

`git clone git@github.com:i5uhail/my-website.git`

**Clone the repo into a folder called website**

`git clone git@github.com:i5uhail/my-website.git website`

---

## Publish back to Git:

`git push`

When the command line does not specify where to push with the < repository > argument, branch.*.remote configuration for the current branch is consulted to determine where to push. If the configuration is missing, it defaults to origin.

`git config --global push.default simple`

`git-fetch` # Download objects and refs from another repository

You can do a git fetch at any time to update your remote-tracking branches under refs/remotes/< remote >/.

This operation never changes any of your own local branches under refs/heads, and is safe to do without changing your working copy. I have even heard of people running git fetch periodically in a cron job in the background (although I wouldn't recommend doing this).

`git pull` # git pull does a git fetch followed by a git merge


```
m-C02SMGEMG8WN:website s0m01cp$ git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)
nothing to commit, working tree clean

m-C02SMGEMG8WN:website s0m01cp$ git push
To github.com:i5uhail/my-website.git
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'git@github.com:i5uhail/my-website.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

m-C02SMGEMG8WN:website s0m01cp$ git fetch
remote: Counting objects: 3, done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 2), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From github.com:i5uhail/my-website
   a91a5ca..040fd49  master     -> origin/master
   
m-C02SMGEMG8WN:website s0m01cp$ git status
On branch master
Your branch and 'origin/master' have diverged,
and have 1 and 1 different commits each, respectively.
  (use "git pull" to merge the remote branch into yours)
nothing to commit, working tree clean

m-C02SMGEMG8WN:website s0m01cp$ git pull
Merge made by the 'recursive' strategy.
 index.html | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)
 
m-C02SMGEMG8WN:website s0m01cp$ git status
On branch master
Your branch is ahead of 'origin/master' by 2 commits.
  (use "git push" to publish your local commits)
nothing to commit, working tree clean

m-C02SMGEMG8WN:website s0m01cp$ git push
Counting objects: 5, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (4/4), done.
Writing objects: 100% (5/5), 591 bytes | 0 bytes/s, done.
Total 5 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To github.com:i5uhail/my-website.git
   040fd49..acdfc20  master -> master
   
m-C02SMGEMG8WN:website s0m01cp$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working tree clean
m-C02SMGEMG8WN:website s0m01cp$

```
---

## Updating Repository and Remote References 

`git remote -v`

`git remote set-url origin git@github.com:i5uhail/website.git`

Sample

```
m-C02SMGEMG8WN:website s0m01cp$ git remote -v
origin	git@github.com:i5uhail/my-website.git (fetch)
origin	git@github.com:i5uhail/my-website.git (push)
m-C02SMGEMG8WN:website s0m01cp$ git remote set-url origin git@github.com:i5uhail/website.git
m-C02SMGEMG8WN:website s0m01cp$ git remote -v
origin	git@github.com:i5uhail/website.git (fetch)
origin	git@github.com:i5uhail/website.git (push)
m-C02SMGEMG8WN:website s0m01cp$
```

Get to know additional information about the remote origin: 

`git remote show origin`

Sample

```
m-C02SMGEMG8WN:website s0m01cp$ git remote show origin
* remote origin
  Fetch URL: git@github.com:i5uhail/website.git
  Push  URL: git@github.com:i5uhail/website.git
  HEAD branch: master
  Remote branch:
    master tracked
  Local branch configured for 'git pull':
    master merges with remote master
  Local ref configured for 'git push':
    master pushes to master (up to date)
m-C02SMGEMG8WN:website s0m01cp$
```

**Get latest from the repo and merge it with the local working directory**

`git status` # below doesnt show any changes and all is up to date. 

`git fetch` # fetches the changes from the repo 

`git pull` # to update your local branch

```
m-C02SMGEMG8WN:website s0m01cp$ git status
On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working tree clean

m-C02SMGEMG8WN:website s0m01cp$ git fetch
remote: Counting objects: 13, done.
remote: Compressing objects: 100% (11/11), done.
remote: Total 13 (delta 5), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (13/13), done.
From github.com:i5uhail/website
   acdfc20..f0be2bb  master     -> origin/master
   
m-C02SMGEMG8WN:website s0m01cp$ git status
On branch master
Your branch is behind 'origin/master' by 5 commits, and can be fast-forwarded.
  (use "git pull" to update your local branch)
nothing to commit, working tree clean

m-C02SMGEMG8WN:website s0m01cp$ git pull
Updating acdfc20..f0be2bb
Fast-forward
 lipsum.txt | 5 +++++
 1 file changed, 5 insertions(+)
 create mode 100644 lipsum.txt
 ```
 ---
 ## Branches on Github
 
 **Creating a branch locally**
 
 `git checkout -b remove-ipsum`
 
 **To switch branches**
 
 `git checkout master`
 
 **To see all branches available**
 
 `git branch -a`
 
 **Delete a branch**
 
 `git branch -d <branch name>`
 
 `git fetch -p`   #Removes any stale branches/tags with prune option of fetch. Example is to remove a branch from the remote and then remove the stale branch from the local working directory. 
 
 Sample
 ```
 m-C02SMGEMG8WN:website s0m01cp$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/master
  remotes/origin/remove-ipsum
m-C02SMGEMG8WN:website s0m01cp$ git fetch -p
From github.com:i5uhail/website
 - [deleted]         (none)     -> origin/remove-ipsum
m-C02SMGEMG8WN:website s0m01cp$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/master
m-C02SMGEMG8WN:website s0m01cp$
```
**To update all tracking branches into master.**
`git pull --all`

**To remove the deleted branches from remote**

`git push origin :<branchName>`

```
m-C02SMGEMG8WN:website s0m01cp$ git branch -d update-readme
Deleted branch update-readme (was 8ddca06).
m-C02SMGEMG8WN:website s0m01cp$ git push origin :update-readme
To github.com:i5uhail/website.git
 - [deleted]         update-readme
m-C02SMGEMG8WN:website s0m01cp$
```

**Pull With Rebase**
[Git - Rebasing](https://git-scm.com/book/en/v2/Git-Branching-Rebasing)

`git pull --rabase`

_Scenario to reproduce:_
Make changes in the remote git repo and simultaneously if a change is made on your local working directory. You can apply git pull --rebase so that it first applies the changes from the remote git and then updates the changes made locally on the remote.

```
* 74183a1 (HEAD -> master) Updating index.html locally before rebase
* 2c083ac (origin/master, origin/HEAD) ReadMe updated from the GitHub GUI
```

```
m-C02SMGEMG8WN:website s0m01cp$ git commit -am "Updating index.html locally before rebase"
[master 7d7b4a7] Updating index.html locally before rebase
 1 file changed, 2 insertions(+), 5 deletions(-)
m-C02SMGEMG8WN:website s0m01cp$ git status
On branch master
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)
nothing to commit, working tree clean
m-C02SMGEMG8WN:website s0m01cp$ git pull --rebase
remote: Counting objects: 3, done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 2), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From github.com:i5uhail/website
   c18eca1..2c083ac  master     -> origin/master
First, rewinding head to replay your work on top of it...
Applying: Updating index.html locally before rebase
m-C02SMGEMG8WN:website s0m01cp$

m-C02SMGEMG8WN:website s0m01cp$ git hist
* 74183a1 (HEAD -> master) Updating index.html locally before rebase
* 2c083ac (origin/master, origin/HEAD) ReadMe updated from the GitHub GUI
* c18eca1 ReadMe updated on Master Github before rebase
* 8ddca06 more edits to readme
* e4265e3 Update readme for new branch
*   dc3e165 Merge branch 'remove-ipsum'
|\
| * b981833 Removing ipsum file
* |   6a96931 Merge pull request #2 from i5uhail/example
|\ \
| |/
|/|
| * 530337b Updated for branch
|/
* f0be2bb deleting demo file
* 82c95a8 Rename demo.txt to md
* 1185af9 Create Demo.txt
*   2aec119 Merge pull request #1 from i5uhail/feature-lipsum
|\
| * 16e7187 Create Lipsum file
|/
*   acdfc20 Merge branch 'master' of github.com:i5uhail/my-website
|\
| * 040fd49 Providing title to ndex
* | 5e44a28 Added Readme file
|/
* a91a5ca Pushing the initialized
* a046d9f Initial commit

```

## Git Graphs:

`git log --oneline --graph`

---
## Tags and Releases

Simple tagging:

`git tag <tagname> <branchname>`

Ex:
`git tag unstable <branchname>`
`git tag stable <branchname>`


Git annotated tags or release tags

`git tag -a <version> -m "<Realese_message>" <commit_id>`

`git tag -a v0.1-alpha -m "release 0.1 (alpha)" commit_id`

Hit show command with tag 

`git show tag v0.1-alpha`

**Pushing Local tags to GitHub**

_Normal `git push` doesnt push the local tags to git hub_

`git push origin stable`

`git push --tags` # to push all tags into repo

Example: 

```
m-C02SMGEMG8WN:website s0m01cp$ git push --tags
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 471 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To github.com:i5uhail/website.git
 * [new tag]         unstable -> unstable
 * [new tag]         v0.1-alpha -> v0.1-alpha
 * [new tag]         v0.2-alpha -> v0.2-alpha
 * [new tag]         v0.3-beta -> v0.3-beta
m-C02SMGEMG8WN:website s0m01cp$
```

**Deleting Tags**

If a tag is already deleted from remote git hub then prune first: 

`git fetch -p`

then 

`git tag -d v0.1-alpha`

Going the other way by deleting the local tag and then pushing to remote

`git tag -d v0.2-alpha`

then 

`git push origin :v0.2-alpha`

**Change Git tag from one commit to other** (Floating tags)

`git tag -f unstable 5dc58d8`

```
m-C02SMGEMG8WN:website s0m01cp$ git tag -f unstable 5dc58d8
Updated tag 'unstable' (was 3f26a6b)
m-C02SMGEMG8WN:website s0m01cp$
```

**If a tag already exists in git remote n it says a conflict!**

`git push --force origin <tagName>`


**To gather new tags/releases from remote**

`git pull`

---

## Comparing on GIT

Are genrally done by using pull request but by not performing the pull request. 

Pointers: 

`develop@{3days}`
`master@{2015-08-13}`

![0.6x5dap9cu2x](/:storage/0.6x5dap9cu2x.png)

# Git - Social Coding

- **Join projects with Forking**
- **Contribute back using forking**
- **Review and accept pull requests**
- **Synchronize our project copy**

NOTE: Upstream Repository is the repository that was forked. 

_At this point we have forked a repo into our personal user space in git and cloned it into our local working directoy. we are creating a new brnach and making mods and pushing it with -u option to set the tracking option in place with the new branch._

```
m-C02SMGEMG8WN:projects s0m01cp$ git clone git@github.com:i5uhail/starter-web.git
Cloning into 'starter-web'...
remote: Counting objects: 39, done.
remote: Total 39 (delta 0), reused 0 (delta 0), pack-reused 39
Receiving objects: 100% (39/39), 261.03 KiB | 111.00 KiB/s, done.
Resolving deltas: 100% (5/5), done.
m-C02SMGEMG8WN:projects s0m01cp$ ls -lrth
total 0
drwxr-xr-x   6 s0m01cp  HOMEOFFICE\Domain Users   204B Mar  3 15:55 demo
drwxr-xr-x  15 s0m01cp  HOMEOFFICE\Domain Users   510B Mar  6 00:11 website
drwxr-xr-x  16 s0m01cp  HOMEOFFICE\Domain Users   544B Mar  6 10:12 starter-web
m-C02SMGEMG8WN:projects s0m01cp$ cd starter-web/
m-C02SMGEMG8WN:starter-web s0m01cp$ ls
404.html				crossdomain.xml				fonts					js
README.md				css					humans.txt				robots.txt
apple-touch-icon-precomposed.png	favicon.ico				index.html				simple.html
m-C02SMGEMG8WN:starter-web s0m01cp$ ls -lrth
total 88
-rw-r--r--  1 s0m01cp  HOMEOFFICE\Domain Users   429B Mar  6 10:12 simple.html
-rw-r--r--  1 s0m01cp  HOMEOFFICE\Domain Users    32B Mar  6 10:12 robots.txt
drwxr-xr-x  5 s0m01cp  HOMEOFFICE\Domain Users   170B Mar  6 10:12 js
-rw-r--r--  1 s0m01cp  HOMEOFFICE\Domain Users   5.0K Mar  6 10:12 index.html
-rw-r--r--  1 s0m01cp  HOMEOFFICE\Domain Users   191B Mar  6 10:12 humans.txt
drwxr-xr-x  6 s0m01cp  HOMEOFFICE\Domain Users   204B Mar  6 10:12 fonts
-rw-r--r--  1 s0m01cp  HOMEOFFICE\Domain Users   766B Mar  6 10:12 favicon.ico
drwxr-xr-x  9 s0m01cp  HOMEOFFICE\Domain Users   306B Mar  6 10:12 css
-rw-r--r--  1 s0m01cp  HOMEOFFICE\Domain Users   603B Mar  6 10:12 crossdomain.xml
-rw-r--r--  1 s0m01cp  HOMEOFFICE\Domain Users   1.2K Mar  6 10:12 apple-touch-icon-precomposed.png
-rw-r--r--  1 s0m01cp  HOMEOFFICE\Domain Users   133B Mar  6 10:12 README.md
-rw-r--r--  1 s0m01cp  HOMEOFFICE\Domain Users   4.4K Mar  6 10:12 404.html
m-C02SMGEMG8WN:starter-web s0m01cp$ git branch
* master
m-C02SMGEMG8WN:starter-web s0m01cp$ git checkout -b feature-readme
Switched to a new branch 'feature-readme'
m-C02SMGEMG8WN:starter-web s0m01cp$ git branch
* feature-readme
  master
m-C02SMGEMG8WN:starter-web s0m01cp$ vi README.md
m-C02SMGEMG8WN:starter-web s0m01cp$ git commit -am "Adding README File"
[feature-readme afd3ccc] Adding README File
 1 file changed, 1 insertion(+), 1 deletion(-)
m-C02SMGEMG8WN:starter-web s0m01cp$ git status
On branch feature-readme
nothing to commit, working tree clean
m-C02SMGEMG8WN:starter-web s0m01cp$ git push -u origin feature-readme
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 323 bytes | 0 bytes/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To github.com:i5uhail/starter-web.git
 * [new branch]      feature-readme -> feature-readme
Branch feature-readme set up to track remote branch feature-readme from origin.
m-C02SMGEMG8WN:starter-web s0m01cp$
```

After this we can create a pull request from git. This by default will be ask for a merge to the upstream repositoty. (All done from the git gui)

While the pull request is still pending users can still contribute to the branch and git will recognie these changes as well. 

See below example: 

```
m-C02SMGEMG8WN:starter-web s0m01cp$ git branch -a
* feature-readme
  master
  remotes/origin/HEAD -> origin/master
  remotes/origin/feature-readme
  remotes/origin/master
m-C02SMGEMG8WN:starter-web s0m01cp$ vi README.md     ## Make more updates to the file
m-C02SMGEMG8WN:starter-web s0m01cp$ git commit -am "Adding README File and edditing it"
[feature-readme d403941] Adding README File and edditing it
 1 file changed, 2 insertions(+)
m-C02SMGEMG8WN:starter-web s0m01cp$ git push
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 348 bytes | 0 bytes/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
To github.com:i5uhail/starter-web.git
   afd3ccc..d403941  feature-readme -> feature-readme
m-C02SMGEMG8WN:starter-web s0m01cp$
```

![0.zyxptgzt7k](/:storage/0.zyxptgzt7k.png)

**Keeping in sync with the fork**

To list the list of remotes: 

`git remote -v`

`git remote add upstream git@github.com:scm-ninja/starter-web.git`

`git remote -v` # to check the additional upstram added to git. 

To make sure its on sync with the fork: 

Pulls the changes from the upstream mentioned in git remote and updates master branch. 

`git pull upstream master`

```
m-C02SMGEMG8WN:starter-web s0m01cp$ git status
On branch feature-readme
Your branch is up-to-date with 'origin/feature-readme'.
nothing to commit, working tree clean
m-C02SMGEMG8WN:starter-web s0m01cp$ git checkout master
Switched to branch 'master'
Your branch is up-to-date with 'origin/master'.
m-C02SMGEMG8WN:starter-web s0m01cp$
m-C02SMGEMG8WN:starter-web s0m01cp$
m-C02SMGEMG8WN:starter-web s0m01cp$ git remote -v
origin	git@github.com:i5uhail/starter-web.git (fetch)
origin	git@github.com:i5uhail/starter-web.git (push)
m-C02SMGEMG8WN:starter-web s0m01cp$ git remote add upstream git@github.com:scm-ninja/starter-web.git
m-C02SMGEMG8WN:starter-web s0m01cp$ git remote -v
origin	git@github.com:i5uhail/starter-web.git (fetch)
origin	git@github.com:i5uhail/starter-web.git (push)
upstream	git@github.com:scm-ninja/starter-web.git (fetch)
upstream	git@github.com:scm-ninja/starter-web.git (push)
m-C02SMGEMG8WN:starter-web s0m01cp$ git pull upstream master
From github.com:scm-ninja/starter-web
 * branch            master     -> FETCH_HEAD
 * [new branch]      master     -> upstream/master
Already up-to-date.
m-C02SMGEMG8WN:starter-web s0m01cp$ git push origin master
Everything up-to-date
m-C02SMGEMG8WN:starter-web s0m01cp$ git branch -a
  feature-readme
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/feature-readme
  remotes/origin/master
  remotes/upstream/master
m-C02SMGEMG8WN:starter-web s0m01cp$ git branch -d feature-readme
warning: deleting branch 'feature-readme' that has been merged to
         'refs/remotes/origin/feature-readme', but not yet merged to HEAD.
Deleted branch feature-readme (was d403941).
m-C02SMGEMG8WN:starter-web s0m01cp$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/feature-readme
  remotes/origin/master
  remotes/upstream/master
m-C02SMGEMG8WN:starter-web s0m01cp$ git fetch -p
```

**Collaborators for a repo**

Adding collaborators to git repo will give them read and write access to the repo

---

## Issues in Github

**Closing an issue with a commit**

Closes issue number 4 with this commit. 

`git commit -m "Ignore Mac OS temp filed, close #4"`

---

## Organization 

Error which indicates: 

error: pathspec 'shared' did not match any file(s) known to git. 

This occurs when a branch is available on both origin and upstream.

`git checkout -b shared origin/shared`

