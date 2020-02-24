
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




---

