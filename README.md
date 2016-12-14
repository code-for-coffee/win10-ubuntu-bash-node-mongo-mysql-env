---
layout: post
title: Install Ubuntu Bash, Node, Mongodb, and MySQL on Windows 10
date: 2016-12-13
tags: windows10,bash,ubuntu,install,node,mysql,mongodb,linux
---

This is a setup guide use Ubuntu Bash on Windows and Linux binaries for applications (versus native Windows applications). This guide has been tested on 64-bit Windows on Windows 10. We're going to use the _apt_ package manager to install a few tools. You might remember using `brew` to do this in Mac OS X earlier during the cohort. Because each environment and application is different, we have provided a few scripts in this repository to help make life easier. Everyone will need to follow steps one; however, steps two, three, and four may be used as needed.

> **Requirements**: Your computer must be running Windows 10 and have a 64-bit processor. The Ubuntu Bash is not available on any prior versions of Windows. 

After completing this installation, note that Bash has a shortcut to to `C:\Windows\System32\bash.exe`. This is actually a symlink to `C:\Windows\WinSxS\amd64_microsoft-windows-lxss-bash_31bf3856ad364e35_10.0.14393.351_none_79648c7a5a883c6f\bash.exe` - in case you want to change out the terminal in an IDE (such as WebStorm).

## Outline

1. Set Windows to Developer Mode
  - Turn on Developer Mode
  - Install Bash
  - Enable Command Line access
  - Creating a Bash shortcut
2. Installing Node.js (LTS v6.0)
3. Installing MongoDB
4. Installing MySQL

## 1. Set Windows to Developer Mode

#### Turn on Developer Mode

* Open the **Settings** application. Note: select the Windows 10 settings app, not Control Panel.
* Search for `Developer` and select `For Developer Settings`. 
* Select 'Developer Mode' to enable it and restart if prompted.

#### Install Bash

* Open **Control Panel**.
* Search for `Windows Features` and select `Turn Windows Features On/Off`. This may be alternatively found under the Programs and Features category.
* Enable (or verify) that **Windows Subsystem for Linux** is enabled and restart if prompted.

#### Enable Command Line access

* Open Powershell with Administrative access.
* _You may do this by right-clicking on Powershell and running as administrator_.
* Inside of Powershell, run the following command:
* `Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux`
* You may be prompted to accept a EULA or install additional features. Say `y` (yes).
* You will need to create a Linux user. This is saved in the traditional user area.
* Name your user and add a password. Linux newbies - you won't be able to see the keys for your password; just hit enter when done.
* Follow any additional prompts if required.

#### Creating a Bash Shortcut

* Search for the **Bash** application your computer.
* Right-click and select **Pin to Start** or **Create Shortcut**
*  From here on out, all commands will be ran inside of Ubuntu Bash.
* We'll install Git and some essential build tools for Linux. Run these commands:

```
apt install git
apt install build-essential
```

## 2. Installing Node.js (LTS v6.0)

This version of node contains most Javasript 2015 (ES6) features availability directly in Node without the need of transpiling. Node isn't included with the standard list of applications available in `apt`. We'll need to add it ourselves:

```bash
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
```

Once completed, we can then install Node by running:

```bash
apt install nodejs
```

You can verify that Node and _npm_ have been installed by running the following commands.

```bash
npm -v
node -v
```

You should see you node version 6 or higher and npm version 3 or higher.

## 3. Installing MongoDB 3.x

MongoDB requires that you add a link to their repositories. It is not hosted publically on `apt`. First, we'll grab that repository, add it to `apt`, and update `apt` so we can install the parts of MySQL that we need.


* Create directories for your MongoDB databases:
* `sudo mkdir /data`
* `sudo mkdir /data/db`
* Import the public key used by the package management system
* `sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv EA312927`
* Create a list file for MongoDB
* `echo "deb http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.2 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.2.list`
* Reload local package database
* `sudo apt update`
* Install MongoDB Specifically
* `sudo apt install mongodb-org`
* Install all components of MongoDB
* `sudo apt install mongodb-org-server`
* `sudo apt install mongodb-org-shell`
* `mongodb-org-mongos`
* `sudo apt install mongodb-org-tools`
* To start your server:
* `sudo service mongodb start`
* Alternatively, you can run the `sudo mongod` command.

To login to MongoDB, you may do so with `mongo`. 

## 4. Installing MySQL

MySQL requires that you add a link to Oracle's repositories. It is not hosted publically on `apt`. First, we'll grab that repository, add it to `apt`, and update `apt` so we can find MySQL. This guide installs MySQL 5.7.

```bash
# get the MySQL repository information
wget http://dev.mysql.com/get/mysql-apt-config_0.8.0-1_all.deb
# install it
sudo dpkg -i mysql-apt-config_0.8.0-1_all.deb
# you'll be provided a GUI option; select the default options (5.7)
# and exit. this is ok! nothing flashy happens here.
# update apt so it can point to the MySQL repository
sudo apt update
```

Once that is installed, we'll install MySQL.

```bash
# install a C library that Ruby uses to build the mysql2 gem with
sudo apt install libmysqlclient-dev
# install mysql
sudo apt install mysql-server
```

Once installed, we can control MySQL with the following commands:

```bash
# start
sudo service mysql start
# stop
sudo service mysql stop
# info
sudo service mysql status
```

To login to MySQL, you may do so with `mysql -p`. `-p` specifies that the user is using a password (so it requests you enter one). 

#### Sources

* https://docs.mongodb.com/v3.2/tutorial/install-mongodb-on-ubuntu/#run-mongodb-community-edition
* https://msdn.microsoft.com/commandline/wsl/install_guide
* https://msdn.microsoft.com/en-us/commandline/wsl/install_guide
