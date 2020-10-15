Adding notes to a commit

git notes add -m 'Tested-by: Johannes Sixt <j6t@kdbg.org>' 72a144e2
git show -s 72a144e

git notes add -m 'My notes'
git notes show

---

Compare the differences between this branch and the HEAD
git diff
git diff HEAD
git diff --cached
git diff otherbranchname
git diff HEAD^ HEAD -> Compares before the last commit and the last commit

---

Restoring files removed from stages/commits:

git restore hello.txt

---

Merge branches fixes and enhancements on top of the current branch, making an octopus merge:

git merge fixes enhancements

---

git reset

---

Removes files from the working tree and index

git rm filename

---

Move or rename a file, a directory, or a symlink

git mv sources destination

---

List, create, or delete branches

$ git branch -d -r origin/todo origin/html origin/man   (1)
$ git branch -D test                                    (2)

Delete the remote-tracking branches "todo", "html" and "man". The next fetch or pull will create them again unless you configure them not to. See git-fetch[1].

Delete the "test" branch even if the "master" branch (or whichever branch is currently checked out) does not have all commits from the test branch.

git branch 'etc' -> creates branch etc.
git branch -> lists all the branches.

---
Run merge conflict resolution tools to resolve merge conflicts

git mergetool

---

Show commit logs

git log

git shortlog

---

Stash the changes in a dirty working directory awa

git stash

git stash push
git stash pop
git stash apply

---

Create, list, delete or verify a tag object signed with GPG

git tag
git tag -a v1.4 -m "my version 1.4"

Tags are ref's that point to specific points in Git history. Tagging is generally used to capture a point in history that is used for a marked version release (i.e. v1.0.1). 

---

Manage multiple working trees

git worktree
git worktree ../myneworktree fromthisbranch

---

Set name 'origin' to that remote repo specified in the url.

git remote add origin https://github.com/jeremythen/test.git

---

Show

git show -> shows the information of the last commit
git show <option> -> option can be a tag, ect.

---

difftool, used to show diffs and to handle them.

git difftool

---

cherry-pick is used to apply a commit (probably in another branch) to the current branch

git cherry-pick commitSha

---


# Notes

Shows the commit history:
> git log

Shows the information of a specific commit:
> git show commit-id

Shows the changes that I made, to make sure I changed what I wanted to change:
> git diff

git hooks are used to check pre commit/push/etc events.

---

Tell git to save the user and password next time they are requested and provided:

> git config --global credential.helper store

