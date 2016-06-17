# Git

## Table of Contents

1. [Why Git](#why-git)
1. [Save Time](#save-time)
1. [Work Offline](#work-offline)
1. [Undo Mistakes](#undo-mistakes)
1. [Don't Worry](#dont-worry)
1. [Make Useful Commits](#make-useful-commits)
1. [Work in your Own Way](#work-in-your-own-way)
1. [Don't Mix Things Up](#dont-mix-things-up)
1. [How to Git](#how-to-git)
2. [Git Pulling and Merging](#git-pulling-and-merging)
3. [Merge Conflicts](#merge-conflicts)

## Why Git?

Although there are dozens of version control systems on the market, some of the world's most renowned projects (like the Linux Kernel, Ruby on Rails, or jQuery) are using Git as their VCS of choice. Here are some of the reasons why.

## Save Time

Git is lightning fast. And although we're talking about only a few seconds per command, it quickly adds up in your work day. Use your time for something more useful than waiting for your version control system to get back to you.

## Work Offline

What if you want to work while you're on the move? With a centralized VCS like Subversion or CVS, you're stranded if you're not connected to the central repository. With Git, almost everything is possible simply on your local machine: make a commit, browse your project's complete history, merge or create branches... Git let's you decide where and when you want to work.

## Undo Mistakes

People make mistakes. A good thing about Git is that there's a little "undo" command for almost every situation. Correct your last commit because you forgot to include that small change. Revert a whole commit because that feature isn't necessary, anymore. And when the going gets tough you can even restore disappeared commits with the Reflog - because, behind the scenes, Git rarely really deletes something. This is peace of mind.

## Don't Worry

Git gives you the confidence that you can't screw things up - and this is a great feeling. In Git, every clone of a project that one of your teammates might have on his local computer is a fully usable backup. Additionally, almost every action in Git only adds data (deleting is very rare). That means that losing data or breaking a repository beyond repair is really hard to do.

## Make Useful Commits

A commit is only really useful if it just contains related changes. Imagine having a commit that contains something from feature A, a little bit of feature B, and bugfix C. This is hard to understand for your teammates and can't be rolled back easily if some of the code is causing problems. Git helps you create granular commits with its unique "staging area" concept: you can determine exactly which changes shall be included in your next commits, even down to single lines. This is where version control starts to be useful.

## Work in Your Own Way

When working with Git you can use your very own workflow. One that feels good for you. You don’t have to be a code acrobat to qualify for using Git. Of course, you can connect with multiple remote repositories, rebase instead of merge, and work with submodules when you need it. But you can just as easily work with one central remote repository like in Subversion. All the other advantages remain – regardless of your workflow.

## Don’t Mix Things Up

Separation of concerns is paramount to keeping track of things. While you’re working on feature A, nothing (and no-one) else should be affected by your unfinished code. What if it turns out the feature isn’t necessary anymore? Or if, after 10 commits, you notice that you took a completely wrong approach? Branching is the answer for these problems. And while other version control systems also know branches, Git is the first one to make it work as it should: fast & easy.

## How to Git

*Assuming you have already installed git on the command line/shell*

![alt text](http://imgs.xkcd.com/comics/git.png
 "Really you just need a few")

To start with the project `git clone [project url]`

Create a new branch `git checkout -b [branch-name]`

Switch to a different branch `git checkout [branch-name]`

Diff you current work and the last commit on your branch `git status`

See previous commits `git log`

Stage your current progress for a commit `git add -A`

Commit your current work `git commit -m [commit message]`

![alt text](http://imgs.xkcd.com/comics/git_commit.png "Commit Messaging")

*Aim for the more discriptive text at the beginning...*

Push your commit to the cloud `git push -u origin [branch-name]`

Pull the current work on the cloud `git pull [branch-url]`

> Pulling and merging tends to be much easier on using a graphical interface for resolving merge conflicts. We make use of [SourceTree](https://www.atlassian.com/software/sourcetree)

Also, it is a good idea to set up aliases for these.  For example, in my bash_profile, I set up an alias `gpo` for `git push -u origin master` - this saves typing.  You can see some of mine [here](https://github.com/keldonia/Dotfiles).

## Git Pulling and Merging

Running `git pull origin [branch]` will fetch the most current version of the branch on the remote repository and then attempt to auto-merge this fetched branch with your current branch, with the most recent changes to a line considered to be the most truthy.  This process can cause a merge conflict when the branch you are working on and the pulled branch have made changes to the same file.  We will try to minimize these potential conflicts by working on different components and areas of the codebase.

## Merge Conflicts

Occasionally, despite our efforts, or due to necessity there will merge conflicts.  You will see these once you attempt pull or merge these conflicting branches.  To resolve these merge conflicts, you will need to follow several steps.  The resolution of these merge conflicts will likely be easier if you are using [SourceTree](https://www.sourcetreeapp.com/download/), which will allow you choose which lines to keep via a GUI.

If you are not using SourceTree follow these steps:
1. You will want to run `git status` to see which files are in conflict.
1. Go in and edit these files, you will typically see something like `<<<<<<HEAD`, some code `==========` some other code `[commit hash]>>>>>>>>`  You will need to manually diff the code between these two sections.
1. If you need to remove any files run the command `git rm -f [file w/ path]` (such as `/client/bundle.js` and `/client/bundle.js.map`)
1. Once you have finished diffing these files, and removing necessary ones run `git status`, this will reveal any files that need to be committed.
1. If these all look fine you can add all of them to your next commit with `git add -A`, else you can add them with `git add [filename]`, else go change the necessary files.
1.  Once satisfied and there are no remaining 'red' files when you run `git status` run `git commit -m '[commit message]'`
