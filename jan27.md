# January 27th Notes

## Two Ways to Access Data

- GUI: graphical user interface (windows explorer, mac finder)
- shell: character-based interface to the OS (command/terminal)
  - we're using git bash: born again shell; incorporated with git

We’re using Git BASH for this course; incorporates git/bitbucket

## Absolute vs Relative Paths

- absolute: typing the exact location starting from the root folder -- `/c/users/student`
- relative: using something like above commands and parameters to nav one-by-one

The `root` is the absolute beginning of a file system.

The `home` folder contains all of a certain user's folders.

## Commands & Parameters (cont.)

- `pwd` - shows your current path / print working directory
- `ls` - lists item within current directory
- `cd foldername` - opens a nested folder
- `cd ..` - goes back one directory / change directory
- `cd ../..` - goes back two directories
- `cd ~` - goes back to user directory, the home folder (`/c/user`)
- `cd .` - not entirely sure
- `mkdir foldername` - creates a directory w/ that name
- `rmdir` - removes a directory / can't recover it
- `cp` - copies a directory/file
  - file: type the name of the file followed by the name of the copy (will have the same content, diff names)
    - `cp mobile-contacts.txt email-contacts.txt`
  - folder: same concept, add `-r`
    - `cp -r Documents Documents-backup`
- `mv` - moves a directory/file
  - type absolute file path followed by destination path
    - `mv ~/Documents/readme.txt ~/Desktop`
  - can also enter the same directory as the file you want to move and simply type the file name followed by the destination name
    - `mv readme.txt ~/Desktop`
- `mv` - same command - renames a file
  - enter the directory, type file name followed by new name
  - `mv readme.txt dontreadme.txt`
- `touch filename.ext` - creates a file
- `code filename.ext` - opens a file in vscode to code
- `cat` - not entirely sure
- `rm` - removes a file (go into dir, `rm filename.ext`)
- up/down arrows allow you to nav through command history
- `cls` - clears screen
- `ls --help` - lists help options

## Version Control

- allows you to go back to previous versions
- saves your progress
- allows others/yourself to see your changes w/ comments

## Git - version control platform

What is git?

- version control system used for tracking changes in files and coordinating files amongst multiple people

Three basic parts:

- local machine: has a local git repository
- git: runs locally
  - allows machine to track files & communicate w/ bitbucket to check for status - is file *a* being updated?
  - all of the changes are saved locally
- remote repository (bitbucket): repository in the cloud
  - local files are only uploaded once you `push` them
  - can also download new files once you `pull` them
  - work w/ repository through git bash

## Creating a Repository

1) Nav to the directory in which you'd like to create the repo.
2) Go to your cloud repo and copy the URL (server where the code is stored)
3) In command line: `git clone <repo url>`

## Entering a Version-Controlled Folder

1) `git status`
   1) shows that status of the repository
   2) lets you know if it's up-to-date/changes were made
   3) tells you if there are *x* # of changes to commit
2) `git pull  master`
   1) `origin` refers to URL address of repository
   2) `master` refers to the project at a very high level

## Moving Files from Local to Repository

1) `git add -A`
   1) stage changes to be pushed up to version control
   2) we want to add a file so we need to get it ready for committing
   3) you'll see a *1* in command line, showing there's one more file to be pushed
   4) the `-A` stands for all
2) `git commit -m "state the changes here for the record"`
   1) pushes the changes to the local repository
3) `git push origin master`
   1) pushes the changes up to the global repository
   2) will always push everything it can push

***Summary: status, pull, add, commit, push***

## Merge Conflicts

If someone else makes a change to something, you the user will have to manually confirm (locally) which is the correct version.