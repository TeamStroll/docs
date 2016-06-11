# Setting Up Your Development Environment

## Install Homebrew - if on a Mac/Linux

Mac:
  First, you are going to need to install [XCode](https://itunes.apple.com/us/app/xcode/id497799835?mt=12).  Don't worry it's free!

  Second, I would recommend using Homebrew - it is a nice package manager for Mac. Simpily run this command: `ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

Linux:
  Run this command to install Linuxbrew: `ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/linuxbrew/go/install)"`

  Then add these lines to your `.bashsrc` or `.zhshrc` file:
  ```bash
  export PATH="$HOME/.linuxbrew/bin:$PATH"
  export MANPATH="$HOME/.linuxbrew/share/man:$MANPATH"
  export INFOPATH="$HOME/.linuxbrew/share/info:$INFOPATH"
  ```

## Set Up Node.js

If you set up Homebrew/Linuxbrew, just run this: `brew install node`

If using [Windows](http://blog.teamtreehouse.com/install-node-js-npm-windows)

Else, if using [Linux](http://blog.teamtreehouse.com/install-node-js-npm-linux)

### Updating Node - if need be

If using Homebrew/Linuxbrew:
  To make sure your brew is current: `brew update`
  To upgrade Node: `brew upgrade node`

If Windows, download the installer and reinstall...

## Install Webpack

You will probably want to install webpack globally.  This can be done using `npm`.  Simply run the following command: `npm install webpack -g`

## Clone the Repo

1. Open up your terminal.
2. `cd [wherever]` to whatever path you want to place your summer work.
3. `mkdir [new folder name]` - whatever you want to name this directory.
4. `cd [new folder name]` into the new directory.
5. `git clone [repo url]`
6. `git checkout [name of current branch]`
7. `git checkout -b [new branch for you]`

Clone the current repo you will be working with.  See Brian, Jordan, or Matt for the password/username.
