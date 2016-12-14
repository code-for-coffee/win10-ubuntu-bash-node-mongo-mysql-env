# Windows 10 Bash + Node Environment Setup

Setup guide + script to setup Ubuntu Bash on Windows.

## Outline

1. Set Windows to Developer Mode
  a. Turn on Developer Mode
  b. Install Bash
  c. Enable Command Line access
  d. Creating a Bash shortcut
2. 

## 1. Set Windows to Developer Mode

#### a. Turn on Developer Mode

* Open **Settings** 
* Search for `Developer` ...
* Select `For Developer Settings`
* _Note: this is the Windows 10 settings app, not Control Panel_
* Select 'Developer Mode' to enable it
* Restart if prompted

#### b. Install Bash

* Open **Control Panel**
* Search for `Windows Features`
* Select `Turn Windows Features On/Off`
* _This may be alternatively found under the Programs and Features category_
* Enable (or verify) that **Windows Subsystem for Linux** is enabled.
* Restart if prompted

#### c. Enable Command Line access

* Open Powershell with Administrative access
* _You may do this by right-clicking on Powershell and running as administrator_
* Inside of Powershell, run the following command:
* `Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux`
* You may be prompted to accept a EULA or install additional features. Say `y` (yes).
* You will need to create a Linux user. This is saved in the traditional user area.
* Name your user and add a password.
* _For Linux newbies - you won't be able to see the keys for your password; just hit enter when done_.
* Follow any additional prompts if required.

#### d. Creating a Bash Shortcut

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
