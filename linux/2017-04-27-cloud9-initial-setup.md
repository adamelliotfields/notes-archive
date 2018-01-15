# Cloud9 Initial Setup
These are my steps for setting up a VM on [Cloud9](https://c9.io), starting with a blank workspace (presently Ubuntu 14.04 Trusty Tahr).  

Cloud9 is great for showing off your app or having a friend collaborate on it with you in realtime. However, you should use Terminal on macOS or PowerShell/Bash-on-Windows for your everyday haxing. Why? Unless you're using a Chromebook, chances are your computer is significantly more powerful than your virtual machine on Cloud9. You're also given a limited amount of space, and `npm install`ing tons of dependencies can fill it up quickly. You should also learn how your own computer works under the hood.  

I've also read on various forums that beginner developers have had issues with Cloud9. I experienced this when I first started writing JavaScript and learning Bash. Here is my solution:  

* There is a massive possibility there is a bug in your code, especially if you just started writing code. Take a deep breath, check for linter errors, and read the stack trace error for which line in your app is throwing the error.
* If it's a server-side app, you probably aren't listening on the right port. You need to use `process.env.IP` and `process.env.PORT`, which are environmental variables set by Cloud9.
* You are using one of Cloud9's templates which installs an older version of Node, as well as a bunch of other programs you won't use. Start with a blank template and add what you need.

Notes:  

*   Do not run `do-release-upgrade` on a free Cloud9 account. It won't work because free accounts do not have enough storage (only 2GB).
*   Do not run `apt-get upgrade` or `apt-get dist-upgrade`. Just upgrade the specific packages you're actually using.
*   When in doubt, you can always just delete your workspace and spin up a new one (clearly I've done this many times).  

### Create a New Workspace  

1. On your dashboard, click "Create a new workspace"
2. Give your workspace a name and an optional description
3. Under templates, click "Blank"
4. Click "Create workspace"  

### Configure Bash Profile
This is my default PATH, which looks for binaries in /usr/local/bin first. We'll be symlinking `/usr/bin/nodejs` to `/usr/local/bin/node`.  

In the Terminal:  

1. Enter `cd ~` (should be `/home/ubuntu/`)
2. Run `nano .bash_profile`
3. Paste `export PATH=/usr/local/bin:/usr/bin:/bin:/usr/local/sbin:/usr/sbin:/sbin`
4. Press `CTRL-X` then press `Y` and then `RETURN` when prompted to exit Nano
5. Back in Terminal, enter `source .bash_profile`
6. Run `echo $PATH` to make sure it worked

### Add Git Completion
Git Completion (formally known as Bash Completion) gives your Terminal tab completion for Git commands. [Here](https://github.com/bobthecow/git-flow-completion/wiki/Install-Bash-git-completion) are the detailed instructions.  

In the Terminal:  

1. Run `sudo apt-get bash-completion`  

### Customize Your Prompt
You can customize your Bash prompt and display Git information in it, thanks to [David Xu](https://github.com/lyze)'s [posh-git-sh](https://github.com/lyze/posh-git-sh) script.  

Check out the repo for more options.  

In the Terminal:  

1. Enter `cd ~`
2. Run `wget https://raw.githubusercontent.com/lyze/posh-git-sh/master/git-prompt.sh`
3. Run `nano .bash_profile`
4. Paste `source ~/git-prompt.sh`
5. Paste `export PROMPT_COMMAND='__posh_git_ps1 "\\[\[\e[0;32m\]\u@\h \[\e[0;33m\]\w" " \[\e[1;34m\]\n\$\[\e[0m\] ";'$PROMPT_COMMAND`
6. Press `CTRL-X` then press `Y` and then `RETURN` when prompted to exit Nano
7. Run `source .bash_profile` and your prompt should change immediately  

By default, your prompt only displays Git information when there are changes. To show information all the time (when you're in a repo folder), add the following to your `.gitconfig` file:  

```
[bash]
  showStatusWhenZero = true
```  

Or enter `git config --global bash.showStatusWhenZero true` from the command line.  

### Install Node
We'll be installing Node, currently v7.9.0.  

In the Terminal:  

1. Run `curl -sL https://deb.nodesource.com/setup_7.x | sudo -E bash -` (this also runs `apt-get update`)
2. Run `sudo apt-get install nodejs`
3. Run `sudo ln -s /usr/bin/nodejs /usr/local/bin/node`
4. Run `node -v` to check your version  

### Install Yarn
I'm using Facebook's [Yarn](https://yarnpkg.com/) to manage project dependencies.  

In the Terminal:  

1. Run `curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -`
2. Run `echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list`
3. Run `sudo apt-get update`
4. Run `sudo apt-get install yarn`
5. Run `yarn --version` to check your version  

### Upgrade Git
Ubuntu comes with Git installed, but you should update it to the latest version.  

In the Terminal:  

1. Run `git --version` to check your current version
2. Run `sudo apt-get install git`
3. Run `git --version` to check the new version  

### Configure Git
Cloud9 should have pre-populated your global `.gitconfig` file with your account info, but you should double check it. Make sure you're in the $HOME directory (`~/`) and run `nano .gitconfig` to make any necessary edits. Here is my starter template:  

```
[user]
  name = Your Name
  email = your@email.address

[core]
  autocrlf = input
  editor = nano -w
```  

### Install Git Extras
[Git Extras]() is a set of helpful Git commands that would normally require multiple sequential commands (as well as Googling Stack Overflow articles). For example, to undo your last commit, simply run `git undo`.  

For some reason, I was only getting version 1.9 when installing from APT (even after an `apt-get update`). For that reason, I'd recommend building from the source.  

In the Terminal:  

1. `cd ~`
2. Run `git clone git clone https://github.com/tj/git-extras.git .git-extras`
3. `cd .git-extras`
4. Run `git checkout 4.2.0` (or whatever the latest [release](https://github.com/tj/git-extras/releases) is)
4. Run `sudo make install`
5. Run `git extras --version` to verify the installed version  

### Install Aptitude
[Aptitude](https://wiki.debian.org/Aptitude) is a command-line front-end for APT. Since Cloud9 is command-line only, you don't have access to Ubuntu GNOME Desktop. Aptitude is better than `apt-get list --installed` to manage your packages.  

In the Terminal:  

1. Run `sudo apt-get install aptitude`
2. Run `aptitude` to run the program
3. Enter `q` to quit  

That's enough to get you started writing some JavaScript apps and pushing them to GitHub. Everything else - like databases and/or libraries/frameworks - can be installed as-needed.  
