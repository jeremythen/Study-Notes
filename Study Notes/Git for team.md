
# Pitfalls

## Untrack pulls

Before making changes to a file, do a pull.
If the changes are already done and you try to pull, then commit your changes and pull.
If there are merging conflicts, resolve them and do a commit and push.


## Forced pushes

Don't do this!

> git push --force

To see all the files:

> git ls-tree --full-tree -r HEAD

# Best Practices

## Commit early, commit often
## Pull frequently

## .gitignore

### To exclude all directories and files with a specific name

* directoryorfilename

### To exclude only directories with a specific name (put a / after the name)
* directoryname/

### Exclude files that end with class

*.class


## Standarizing line ending with *autocrlf

> git config autocrlf input

This will turn CRLF to LF, for platform compatibility.

## Branch Name

> git branch -b bug/123/menue-issue

Basically, this naming convention can help you create a branch name easy to understand what it is about.

## Descriptive commit massages

Avoid using the -m flag to add a commit message. Instead, use a text editor.
To set up an specific text editor:

> git config --global core.editor "path/to/the/texteditor"

Then, commit without the -m flag

> git commit

To set up a commit template

> git config commit.template "path/to/the/.templatefile.txt"


## Team Composition and member roles

* Maintainer
    * Perform Commits
    * Integrates pull requests
    * Inherits contributor permissions

* Contributor
    * Clones repositories
    * Lacks commit privilages (to the main branch, they do commits to their own private copy)
    * Submits pull requests

For small size team (2 o 3), all of them could have full read and write access to the repository.

For midsize team you can have a maintainer that can read and write to the **Central Repository**, and contributors that request the maintainer pull requests.

For large teams, you can have several maintainers and a lot of contributors.

For some teams, a Dictator Repository could be neeaded. Who is the maintainer above maintainers.

## Defining contributor and maintainers standards

_Maintainer/Contributor Guidelines for x project_

Documment their actions, coding standrad, guides, information, code of conduct, etc.


# Remote Platforms

* Gitlab
* Github
* Bitbucket

> git init --bare my-project.git

The **--bare** flag creates a repository that doesn’t have a working directory, making it impossible to edit files and commit changes in that repository. You would create a bare repository to git push and git pull from, but never directly commit to it. Central repositories should always be created as bare repositories because pushing branches to a non-bare repository has the potential to overwrite changes.


---

# Terms

* Gists
* Find Bug Analizer (maven pluging)

---

## Long-Running Branches

* Master (main branch that at the end, will receive the changes from Develop).
* Develop (current branch receiving all the changes).


## Feature Branches

* Branches to work usually on 1 feature, merged to Develop and then closed.

## Hotfix Branches

* Branch to quickly apply a patch to a production environment. (Branch from the master, fix it, and then merge with master).

# Workflows

## Trunk-based workflow (TBD)

* Single long-lived branch.
* Updates and pulls occur from a single branch named Trunk.
* Commits by contributors on the trunk branch.
* Trunk branch always ready for production.

## Git flow

* Control is handled by Maintainers
* Master branch, Develop branch, Feature branch, Hotfix branch are supported here.
* Pull and merge requests from contributors.

---

# Milestones

* Organize issues for a project

---

When the changes in Develop are ready to be merged with Master, create another branch from Develop, like: "release-1", do testing on it, edit it if needed and merge that to Master.

You can also merge Master to Develop to have any other changes that Master may have and develop doesn't.

---

# Gitlab Runner

* A CI/CD service.

Create a file named:

**.gitlab-ci.yml**

This file is the Gitlab Runner pipiline.

In that file:

````
build:
    script:
        -mvn compile
````







