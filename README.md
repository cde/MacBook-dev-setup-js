# Mac OS X Dev Setup

This document describes how I set up my basic javascript developer environment on a new MacBook from scratch.
It's pretty much a continuation of my [ruby developer env](https://github.com/cde/MacBook-dev-setup-ruby).
The steps below were tested on OS X El Capitan.

I will set up [nodejs](https://nodejs.org). I'm assuming you have followed and/or installed:

- [System update](#system-update)
- [Install your favorite editor](#install-your-favorite-editor)
- [iTerm2](http://www.iterm2.com/)
- [Install your favorite browser](https://github.com/cde/MacBook-dev-setup-ruby#install-your-favorite-browser)
- [XCode CommandLine Tools](#xcode-commandline-tools)
- [Homebrew](#homebrew)
- [Git](#git)
- [Node.js](#node-js)
- [Heroku](https://github.com/cde/MacBook-dev-setup-ruby#heroku)
- [Setting Up A Database](#setting-up-a-database)


## System update
It's always a good idea to Update the system :p. For that: **Apple Icon > Software Update...**

## Install your favorite editor

Everyone has their preferences. I'll leave it up to you. Download and install your preference. Here there are some options I have personally used:
- [Atom](https://atom.io/) (free)
- [Brackets](http://brackets.io/) (free)
- [Sublime](http://www.sublimetext.com) (paid)
- [Vim](http://www.vim.org/) (free)

Although [Webstorm](https://www.jetbrains.com/webstorm/) is a paid javascript IDE, it's pretty light and popular too.

## XCode CommandLine Tools

**Command Line Tools** for **Xcode** is an important dependency before Homebrew can work. These include compilers that will allow you to build things from source.

Unless you're developing iPhone or Mac apps, you only need to install the Command Line Tools, without Xcode. You can go to [http://developer.apple.com/downloads](http://developer.apple.com/downloads), and sign in with your Apple ID, and search for "command line tools" and download the latest **Command Line Tools (OS X 10.11) for Xcode 7.3.1** (my version Jun 2016).

## Homebrew
Package managers make it so much easier to install and update applications (for Operating Systems) or libraries (for programming languages). I use the popular one for OS X  [Homebrew](http://brew.sh/).

### Install

In the terminal prompt paste the following line , hit Enter, and follow the steps on the screen:

    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
Add  `/usr/local/bin` to your `$PATH` environment variable:

    echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.bash_profile

Run the following command to make sure everything works:

    brew doctor

Now that we have Homebrew installed, we can use it to install packages.

***Note***

You can start or stop any services with

    brew services start <mongodb/redis/postgresql>

    brew services stop <mongodb/redis/postgresql>

## Git

I'll be using Git for version control system and [Github](https://github.com/) repo. ***You will need to create a Github account if don't have already one.***

    brew install git

When done, to test that it installed fine you can run:

    git --version

And `$ which git` should output `/usr/local/bin/git`.   

### Basic configuration

The [first thing](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup#_first_time) you should do when you install Git is to set your user name and email address.

    git config --global user.name "YOUR NAME"
    git config --global user.email "YOUR@EMAIL.com"

This will add user info to **.gitconfig** file in your home directory. I have some more about basic configuration [here](https://github.com/cde/MacBook-dev-setup-ruby#git) .

### Configure Github
The next step is to generate a SSH key and add it to your Github account.

    ssh-keygen -t rsa -C "YOUR@EMAIL.com"

Copy and paste the output of the following command and [paste it here](https://github.com/settings/ssh)
    cat ~/.ssh/id_rsa.pub

You can check and see if it worked:  

    ssh -T git@github.com

You should get a message like this
    **Hi <your username>! You've successfully authenticated, but GitHub does not provide shell access.**    

# Node.js

To install Node.js there are a couple alternatives

-  NVM

I like to install [node.js](https://github.com/nodejs/node) using [Node Version Mananger](https://github.com/creationix/nvm). Open the previous link and follow the instructions of your preferences. The easy way is to use  the **install script** [nvm v031.1](https://github.com/creationix/nvm/blob/v0.31.1/install.sh) similar to:

    curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.1/install.sh | bash

or

    wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.31.1/install.sh | bash


**Note**: if you don't have wget you can install it with:

    brew install wget


***The script clones the nvm repository to ~/.nvm and adds the source line to your profile (~/.bash_profile, ~/.zshrc, ~/.profile, or ~/.bashrc).***


To verify that nvm has been installed, do:

    command -v nvm


-  You can also install it with:


    brew update

    brew install node


- Or download pre-built [installer](https://nodejs.org/en/) for your platform.

## Npm
Npm is the package manager for JavaScript. It's installed when you install Node.js

To install a package:

    npm install <package> # Install locally
    npm install -g <package> # Install globally

To install a package and save it in your project's `package.json` file:

    npm install <package> --save

To see what's installed:

    npm list # Local
    npm list -g # Global

To find outdated packages (locally or globally):

    npm outdated [-g]

To upgrade all or a particular package:

    npm update [<package>]

To uninstall a package:

    npm uninstall <package>

## io.js    

[io.js](https://iojs.org) has merged with the Node.js. All of the features in io.js are available in Node.js v4 and above.    

# Setting Up A Database

## MongoDB

[MongoDB](http://www.mongodb.org/) is a popular [NoSQL](http://en.wikipedia.org/wiki/NoSQL) database.

### Install

I like to install it through Homebrew:

    brew update
    brew install mongo

Follow the instructions:

To have launchd start mongodb now and restart at login:

    brew services start mongodb
Or, if you don't want/need a background service you can just run:

    mongod --config /usr/local/etc/mongod.conf    

### Usage

In a terminal, start the MongoDB server:

    mongod

In another terminal, connect to the database with the Mongo shell using:

    mongo

Refer to MongoDB's [Getting Started](http://docs.mongodb.org/manual/tutorial/getting-started/) guide for more!


## Redis

[Redis](http://redis.io/) is an in-memory **data structure store**. Redis stores the data in a key-value structure.

### Install

To install Redis, use Homebrew:

    brew update
    brew install redis

Then follow the instructions of your preference:

    #To have launchd start redis now and restart at login:

    brew services start redis

    #Or, if you don't want/need a background service you can just run:

    redis-server /usr/local/etc/redis.conf    

### Usage

Start a local Redis server using the default configuration settings with:

    redis-server

For advanced usage, you can tweak the configuration file at `/usr/local/etc/redis.conf` (I suggest making a backup first), and use those settings with:

    redis-server /usr/local/etc/redis.conf

Connect to the server with the Redis command-line interface using:

    redis-cli

For more information Redis' [documentation](http://redis.io/documentation).

## Other DB
Information about setting up [PostgreSQL](https://www.postgresql.org/) and [MySQL](http://www.mysql.com/) can be found [here](https://github.com/cde/MacBook-dev-setup-ruby#setting-up-a-database).
