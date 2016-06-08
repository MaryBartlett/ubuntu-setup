# ubuntu-setup
The way I like to set up my laptop

**Installing Ubuntu**

You will need a laptop, and a USB key containing a bootable Ubuntu installation.

    * Boot from the USB containing the Linux installation.
    * Go through the setup wizard.
    * Under Preparing to install Ubuntu, you can choose to Install this third-party software.
    * Under Wireless, confirm you don't want to connect to the wi-fi network right now.
    * Under Installation type, choose to Encrypt the new Ubuntu installation for security (you'll shortly need to provide a password for this), and Use LVM with the new Ubuntu installation. (if you want you can create your own partitions)
    * In the following pages, specify your location and keyboard layout.
    * Under Who are you?, specify a computer's name (can be the code on your laptop), a username (easier if this matches your NOE username), and password. (As you have encrypted the entire drive, you don't need to choose Encrypt my home folder).
    * When complete, your machine will hopefully ask you to restart into the desktop UI.
    * Plug the network cable back


**Reminder! You should select:**
* Install this third-party software
* Encrypt the new Ubuntu installation for security
* Use LVM with the new Ubuntu installation


**﻿Install vim**

`sudo apt-get install vim`

**Install git**

`sudo apt-get install git`

**Make /bin in ~/**

`cd ~/`

`mkdir bin`

This is where all programmes will be installed to

**In ~/.bashrc, (`vi ~/.bashrc`) add**

`export PATH=~/bin:$PATH`

(to get these changes, type `bash` – otherwise this doesn't get updated)

**Install sublime**

http://www.sublimetext.com/3

Download tar.bz2

Run:  `tar -vxjf sublime_text_3_build_3083_x63.tar.bz2` or whatever version you have installed

Move the extracted folder to whereever you want to keep your programmes (in this case, ~/bin)

`sudo mv sublime_text_3 ~/bin/`

Then in ~/bin, make a sym-link to sublime (I've called it subl, call it whatever you like)

`ln -s sublime_text_3/sublime_text subl`

To get a desktop icon

`cd /usr/share/applications`
vi sublime.desktop

Copy these contents in (don't forget to change the Icon path)

```
[Desktop Entry]
Version=1.0
Name=Sublime Text 3
*#Only KDE 4 seems to use GenericName, so we reuse the KDE strings.*
*#From Ubuntu's language-pack-kde-XX-base packages, version 9.04-20090413.*
GenericName=Text Editor
Exec=sublime
Terminal=false
Icon=/home/<user>/bin/sublime_text_3/Icon/48x48/sublime_text.png
Type=Application
Categories=TextEditor;IDE;Development
X-Ayatana-Desktop-Shortcuts=NewWindow
[NewWindow Shortcut Group]
Name=New Window
Exec=sublime -n
TargetEnvironment=Unity
```
Then `subl` and lock to launcher

To install package manager https://packagecontrol.io/installation

**Install nvm (node)**

https://github.com/creationix/nvm

To install NVM in ~/bin, run:

    git clone https://github.com/creationix/nvm.git ~/.nvm && cd ~/.nvm && git checkout `git describe --abbrev=0 --tags`

Add to bashrc

`source ~/.nvm/nvm.sh`

And again to make sure the bash updates run: `bash`

To get a node version

`nvm install 5.3.0` (and whichever version it installs, set that as the default)
`nvm alias default 5.3.0`
Now you should also have npm installed - but it will be an old version, so run

`npm install -g npm@3.3.12`

You can now install grunt (globally)

`npm install -g grunt-cli`

And gulp

`npm install -g gulp`


**Setup git**

https://help.github.com/articles/set-up-git/

Probably prefer clone with ssh - https://help.github.com/articles/generating-ssh-keys/

To check whether it's worked, run: `ssh -T git@github.com`

Also add your ssh key to github.com


**Nginx**

`sudo apt-get install nginx-core`

If when you try to run nginx you get an error about access and error logs:

nginx: [alert] could not open error log file: open() "/var/log/nginx/error.log" failed (13: Permission denied)
2015/07/21 13:36:02 [warn] 32093#0: the "user" directive makes sense only if the master process runs with super-user privileges, ignored in /etc/nginx/nginx.conf:1
2015/07/21 13:36:02 [emerg] 32093#0: open() "/var/log/nginx/access.log" failed (13: Permission denied)
Changed the ownership of the access and error logs by going to /var/log/nginx and then running

In var/log/nginx

`sudo chown <user>:<user> error.log`
`sudo chown <user>:<user> access.log`

You might have to restart

`sudo service nginx restart`

Make sure in your /etc/nginx/nginx.conf you have changed “YOUR_CERT_PATH” to be /etc/nginx/certs/ and “YOUR_WORKSPACE_PATH” to be e.g. /home/mbartlet/code


**PhantomJS**

To download

https://bitbucket.org/ariya/phantomjs/downloads/

phantomjs-1.9.8-linux-x86_64.tar.bz2

Extract it `tar vxjf phantomjs-1.9.8-linux-x86_64.tar.bz2`

Move to bin `mv phantomjs-1.9.8-linux-x86_64 ~/bin/phantomjs-1.9.8`

Create a sym link `ln -s phantomjs-1.9.8/bin/phantomjs phantomjs` (it's important the sym link is called phantomjs)


**Install Chrome**

https://www.google.co.uk/chrome/browser/desktop/

Download

Open ubuntu software centre

Install Chrome

**Install terminator**

https://apps.ubuntu.com/cat/applications/precise/terminator/



**Other things you might need as a web dev**

**Install rvm (ruby)**

https://rvm.io/rvm/install

You might have to install curl `apt-get install curl`

Once installed (and you've run source /home/<user>/.rvm/scripts/rvm so you can use it in the current terminal session)

Set this in your ~/.bashrc

`export PATH="$PATH:$HOME/.rvm/bin"`

`[[ -s "$HOME/.rvm/scripts/rvm" ]] && source "$HOME/.rvm/scripts/rvm" # Load RVM into a shell session *as a function*`

Install ruby versions

`rvm install 2.2.2`

Set your default ruby

`rvm use 2.2.2 --default` (you might have to run `/bin/bash --login` beforehand)

**Install caseprjs**

``npm install -g casperjs``

**Install nodemon**

``npm install -g nodemon``

**Install virtual box**

Download virtual box following the instructions [here](https://help.ubuntu.com/community/VirtualBox/Installation)

Download the e.g. Windows version you want from modern.ie [here](https://dev.windows.com/en-us/microsoft-edge/tools/vms/linux/)

Move your e.g. Windows 8.1 ova somewhere you're happy with it

Open Virtual Box (I installed Virtual Box from ubuntu repositories so I know my instructions work for that, but I assume it works for Oracle download too). Go to file, Import appliance, and navigate to where you've saved the .ova file, click next and import.

Don't forget to take a snapshot as these VMs run out after 90 days and the snapshot will help you!

You'll need to add localhosts if you want to be able to access your localhost through your VM. Open notepad as an administrator and then edit your `C:\Windows\System32\drivers\etc\hosts` file. Add the following to this file (each time you turn off your laptop you might have to change your hosts file to use your new IP), where 10.57.40.29 is the inet addr you get after ifconfig on your Ubuntu box.

```
10.57.40.29       localhost
```

Now restart IE if you've had it open (it caches the hosts file) and then localhost should load.

**Clojure**

**JDK (JAVA)**

http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html

jdk-8u51-linux-x64.tar.gz

Accept license

Download it

Extract `tar -vxzf jdk-8u51-linux-x64.tar.gz`

Move to ~/bin  `mv jdk1.8.0_51/ ~/bin/`

Set up sym links in ~/bin

`ln -s jdk1.8.0_51/bin/java java && ln -s jdk1.8.0_51/bin/javac javac`


**Leiningen**

http://leiningen.org/

Make sure you have Java installed first!

Make file lein in ~/bin

Copy the script from leiningen.org into there

Make it executable `chmod u+x lein`

Run lein and you'll have it installed


**Debugging**


If you ever see the ENOSPC error:

http://stackoverflow.com/questions/16748737/grunt-watch-error-waiting-fatal-error-watch-enospc