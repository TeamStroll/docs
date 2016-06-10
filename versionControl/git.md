# Git

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

Aim for the more discriptive text at the beginning...

Push your commit to the cloud `git push -u origin [branch-name]`

Pull the current work on the cloud `git pull [branch-url]`

> Pulling and merging tends to be much easier on using a graphical interface for resolving merge conflicts. We make use of [SourceTree](https://www.atlassian.com/software/sourcetree)

Also, it is a good idea to set up aliases for these.  For example, in my bash_profile, I set up an alias `gpo` for `git push -u origin master` - this saves typing.  You can see some of mine [here](https://github.com/keldonia/Dotfiles).
