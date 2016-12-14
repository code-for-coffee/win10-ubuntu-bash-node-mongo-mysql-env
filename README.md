# Windows 10 Bash + Node, Mongodb, and MySQL Environment Setup

Setup guide + script to setup Ubuntu Bash on Windows.

## Outline

1. Set Windows to Developer Mode
  - Turn on Developer Mode
  - Install Bash
  - Enable Command Line access
  - Creating a Bash shortcut
2. Installing Node.js (LTS v6.0)
3. Installing MongoDB
4. Changing your WebStorm Shell Preferences

## 1. Set Windows to Developer Mode

#### Turn on Developer Mode

* Open **Settings** 
* Search for `Developer` ...
* Select `For Developer Settings`
* _Note: this is the Windows 10 settings app, not Control Panel_
* Select 'Developer Mode' to enable it
* Restart if prompted

#### Install Bash

* Open **Control Panel**
* Search for `Windows Features`
* Select `Turn Windows Features On/Off`
* _This may be alternatively found under the Programs and Features category_
* Enable (or verify) that **Windows Subsystem for Linux** is enabled.
* Restart if prompted

#### Enable Command Line access

* Open Powershell with Administrative access
* _You may do this by right-clicking on Powershell and running as administrator_
* Inside of Powershell, run the following command:
* `Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux`
* You may be prompted to accept a EULA or install additional features. Say `y` (yes).
* You will need to create a Linux user. This is saved in the traditional user area.
* Name your user and add a password.
* _For Linux newbies - you won't be able to see the keys for your password; just hit enter when done_.
* Follow any additional prompts if required.

#### Creating a Bash Shortcut

* Search for the **Bash** application your computer.
* Right-click and select **Pin to Start** or **Create Shortcut**
* You'll be using the Bash terminal from here on out!

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

> This process is a bit complicated; code snippets are available to copy and paste as individual lines.

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
* To start your server, you can run the `sudo mongod` command.
* In another terminal window/tab, you can connect to your server using `mongo`.
