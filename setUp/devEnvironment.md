# Setting Up Your Development Environment

## A Note on Google Drive

  ![alt text](http://imgs.xkcd.com/comics/old_files.png "Don't sync everything")

  You probably don't want to sync everything.  A lot of it is extraneous to your purposes.

## Install Homebrew - if on a Mac/Linux

Mac:
  - Install [XCode](https://itunes.apple.com/us/app/xcode/id497799835?mt=12).  Don't worry it's free!

  - I would recommend using Homebrew - it is a nice package manager for Mac. Simpily run this command: `ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

Linux:
  - Run this command to install Linuxbrew: `ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/linuxbrew/go/install)"`

  - Then add these lines to your `.bashsrc` or `.zhshrc` file:
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

A small dependency for browser compatability, browserslist, should also be installed: `npm install browserslist -g`

## Install Java

Type install [Java](https://java.com/en/download/help/index_installing.xml) into google, and install it.

## Install MySQL - if on the backend

I hope you installed brew, as you just have to run:

`brew install mysql`

Create a username

To log in run `mysql -u root -p`  the password you setup in install.

sftp into the server ask Brian where the data dump is.

Then you will need to create a table in mysql.  Once logged into mysql, you will want to create a table using the command: `CREATE TABLE sbe;`.

Once this is done you will want to exit out of mysql and run the following command: `mysql -u root -p sbe < [data dump]`.

In mysql, run `use sbe`.

You can then see all the tables by running: `SHOW TABLES;`

## Open project in Eclipse or other IDE

For the backend, open it in [Eclipse](https://www.eclipse.org/downloads/) or another IDE of choice.  Import the sh_repo as a Maven project and then navigate to 'sh_repo/applications/webApps/' and open 'platform'.  Once imported you should be good to go, hopefully...

Once imported, you want to navigate to: 'src/main/java/com/sh/platform/', you then run a local backend via running 'Main.java', it will take a while to build to this the first time.  See backend for further details.

## Browser

Install [Chrome](https://www.google.com/chrome/)

If frontend, install the [React Developer Tools](https://chrome.google.com/webstore/detail/react-developer-tools/)


## Clone the Repo

1. Open up your terminal.
2. `cd [wherever]` to whatever path you want to place your summer work.
3. `mkdir [new folder name]` - whatever you want to name this directory.
4. `cd [new folder name]` into the new directory.
5. `git clone [repo url]`
6. `git checkout [name of current branch]`
7. `git checkout -b [new branch for you]`

Clone the current repo you will be working with.  See Brian, Jordan, or Matt for the password/username.

![alt text](http://imgs.xkcd.com/comics/identity.png "Your password")
