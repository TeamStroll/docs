# Git

## Why Git and Version Control?

Git is powerful tool in that it allows to track changes to our code base, and work on specific sections of the codebase *without* altering the production/qa branches while building and testing locally.  It also enables to quickly rollback changes and co-operate more easily.  It does this by diffing different bodies of code and reconciling them in merges. It also allows us to easily distribute code between ourselves and get the most recent updates.

Most of our code lives on Bitbucket, though these docs are hosted on Github.  The primary difference between the two is which we are communicating with!

## How to Git

*Assuming you have already installed git on the command line/shell*

![alt text](https://xkcd.com/1597/ "Really you just need a few")

To start with the project `git clone [project url]`

Create a new branch `git checkout -b [branch-name]`

Switch to a different branch `git checkout [branch-name]`

Diff you current work and the last commit on your branch `git status`

See previous commits `git log`

Stage your current progress for a commit `git add -A`

Commit your current work `git commit -m [commit message]`

![alt text](https://xkcd.com/1296/ "Commit Messaging")
Aim for the more discriptive text at the beginning...

Push your commit to the cloud `git push -u origin [branch-name]`

Pull the current work on the cloud `git pull [branch-url]`

> Pulling and merging tends to be much easier on using a graphical interface for resolving merge conflicts. We make use of [SourceTree](https://www.atlassian.com/software/sourcetree)
