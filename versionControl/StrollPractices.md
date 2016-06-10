# Stroll Version Control Policies

Most of our code lives on Bitbucket, though these docs are hosted on Github.  The primary difference between the two is which we are communicating with!

## General Policies

- When you begin work on a new feature or start work on fixing a bug, checkout a new branch.  Why?  This means you are not working on the main branch and easily shift back to the unaltered branch if things do not work as expected. It also makes identifying the sources of bugs easier.
- When you are working commit early and often! Why? This will allow you reset to a previous commit, where things were working. (use `git reset --soft HEAD^` if you want to keep your changes and `git reset --hard HEAD^` if you want to nuke the commit and remove the changes)

## Front End

- When you are done with your work push your *branch* to the repo.  Following this there will be a code review *before* the branch is merged in to the main branch.
