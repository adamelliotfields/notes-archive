# Windows JavaScript Development Environment

*Also see the "official" [guide](https://github.com/Microsoft/nodejs-guidelines/blob/master/windows-environment.md#compiling-native-addon-modules) from Microsoft.*

If you're just getting started, here are my suggestions for getting a dev environment set up on Windows.    

### Install Ubuntu on Windows
You'll be doing all of your work in PowerShell, but you should still install Ubuntu as it's pretty awesome that you no longer need to dual-boot or run a virtual machine to get Linux on a Windows PC.  

[How to Install and Use the Linux Bash Shell on Windows 10](https://www.howtogeek.com/249966/how-to-install-and-use-the-linux-bash-shell-on-windows-10/)  

If you don't want to install Ubuntu on Windows, but want to experiment with the Linux command line, you should definitely create a free account on [Cloud9](https://c9.io). Check out my Gist [here](https://gist.github.com/adamelliotfields/95abdfb69ddbfeccabc7b831a92c790f).  

### Set the PowerShell shortcut to run as Admin
PowerShell is a command line shell and scripting language built on Microsoft's .NET framework. It gives you more power than the standard Command Prompt through the use of system administration tasks called [cmdlets](https://technet.microsoft.com/en-us/library/ee332526.aspx).  

Cmdlets have aliases, and in many cases they are equivalent to their Bash counterparts. For example, `Get-Process` is aliased `ps`; while `Stop-Process` is aliased `kill`. `mkdir`, `ls`, `cp`, `mv`, and `rm` all work - but there is no `touch` (you'd want to use `New-Item` or `ni` instead).  

There is also a [gallery](https://www.powershellgallery.com/) of PowerShell modules you can peruse. A popular one is [PSReadLine](https://www.powershellgallery.com/packages/PSReadline).  

Do you use iTerm on macOS or Terminator on Linux? Check out [ConEmu](https://conemu.github.io/) for PowerShell.  

Running Powershell as Admin is loosely analogous to running Bash as root. If you don't want to do this and you run into an issue where a task requires elevated privileges, run `Start-Process -FilePath "powershell.exe" -Verb runAs` to open a new Powershell window as Admin (or just right-click the Powershell shortcut and run as Admin).  

1. Go to `$HOME\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Windows PowerShell`
2. Right-click Windows PowerShell.
3. Click Properties.
4. Click Shortcut.
5. Click Advanced.
6. Click "Run as administrator".  

### Install Chocolatey
[Chocolatey](https://chocolatey.org/) is a Windows package manager, similar to Homebrew on macOS. The main benefit of Chocolatey is that you can install your programs easily from within PowerShell, as opposed to going to the program's website, downloading the executable, and then running it. Chocolatey will also take care of updating and uninstalling programs.  

If you do install a program using Chocolatey that has an auto-update feature, you should disable it and use Chocolatey to manage updates. Chocolatey does have a sync feature available on their paid plans (starting at $8/mo), so if you make a change outside of Chocolatey, it keeps everything nice and tidy.  

The biggest downside to Chocolatey is that each package is maintained by a volunteer (which in-and-of-itself is awesome from an open source community aspect). Some packages get updated within a couple days of the latest release; some packages never get updated. Just like with any open source project, if it's abandoned, you probably don't want to use it.  

You may have heard of PowerShell's built-in package manager known as OneGet. OneGet still needs to use Chocolatey as a registry for packages, and the Chocolatey FAQs advise against doing this.  

1. Open PowerShell as Admin.
2. Run `Set-ExecutionPolicy Bypass`
3. Run `iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))`  

### Install Chocolatey GUI
`choco install chocolateygui`  

I personally love Cakebrew on macOS, and the Chocolatey GUI works similarly.  

### Install Git
`choco install git.install`  
`choco install git`  
`choco install poshgit`  

This installs [Git for Windows](https://git-for-windows.github.io/), which also installs Git GUI and Git Bash. Git Bash is a Bash emulator, but I run all my Git commands in Powershell and you should too. The first time you `git push` to GitHub, a window will pop up asking for your GitHub username and password. Git for Windows will remember this, so you shouldn't need to enter it again.   

[poshgit](http://dahlbyk.github.io/posh-git/) adds Git information to your POwerSHell prompt so it will look like this (except colored):  

`C:\Users\Adam\GitHub\repo [master ≡ +1 ~0 -0 !]>`  

You'll also get tab completion within PowerShell for Git commands.  

You should also install TJ Holowaychuk's [Git Extras](https://github.com/tj/git-extras). This will give you access to commands like `git undo` to undo your last commit. Follow the instructions [here](https://github.com/tj/git-extras/blob/master/Installation.md) to install.  

### Configure Git
Read my Gist [here](https://gist.github.com/adamelliotfields/60415694ca2a511dcaeb4e3be78017b4).  

### Install Git Kraken
[Git Kraken](https://www.gitkraken.com/) is a GUI for Git that is better than Github Desktop or Git-for-Windows GUI, in my opinion.  

Git Kraken has a neat feature that watches an entire folder of Git repositories (all my repos are in my `GitHub` folder, some people use a folder named `Projects`; just don't use the folder called `Dropbox`). I can simply see which repositories are behind, and pull the repo I plan to work on.  

I recommend installing Git Kraken outside of Chocolatey so it can manage its own updates.  

### Node Version Management
Before you install Node and Yarn, you may want to consider installing a Node version management tool. The most popular - `nvm` and `n` - will unfortunately not work on Windows. There are two options then: `nvm-windows` and `nodist`. [nvm-windows](https://github.com/coreybutler/nvm-windows/) is the newest and has the most stars on GitHub, so that's the one I'm using. `nvm-windows` is written in Go, whereas `nodist` is written primarily in JavaScript.  

Why would you want to use a Node version management tool? Because you might find yourself in the situation I'm in now, where my Node 7.9.0 app isn't working for anyone I've shown it to because they are using older versions of Node. I can cycle between versions of Node using the `nvm use` command in PowerShell, run my app, and make sure it works.  

If you do use `nvm-windows` or `nodist`, **DO NOT** install Node separately! You'll be using your version manager to handle installing and uninstall Node.  

You can download the `nvm-windows` installer from the repo and follow the installation process.Then go into PowerShell to install Node. To install version 7.9.0, simply run `nvm install 7.9.0` followed by `nvm use 7.9.0`.  

If you decide you want to use a version manager in the future, just know that you'll have to completely remove Node from your computer, as well as your npm folder and all globally installed packages.  

Lastly, do not install Yarn using Chocolatey (or anything that requires Node from Chocolatey), as they will install the NodeJS.org installer of Node and that will mess up your NVM installation.  

### Install Node
`choco install nodejs.install`  
`choco install nodejs`  

You can install Node using Chocolatey if you decide not to use a Node version management tool.  

### Install Yarn
`choco install yarn`  

[Yarn](https://yarnpkg.com/) is a package manager developed by Facebook in collaboration with Google, Tilde, and Expo. It offers performance improvements over NPM, while still using the NPM registry and `package.json`.  

If you are using a Node version management tool, do not install Yarn via Chocolately. You can use NPM to install Yarn, which will bind Yarn to the version of Node that is currently in use: `npm install --global yarn`. Since Yarn is a Node application, it makes sense to use Node's package manager to install and update it.  

Alternatively, you can use the traditional installer found [here](https://yarnpkg.com/lang/en/docs/install/#windows-tab).  

### Install Velocity
`choco install velocity`  

[Velocity](https://velocity.silverlakesoftware.com/) is the Windows equivalent of Dash on macOS or Zeal on Linux. It allows you to store documentation offline and quickly search for anything. Velocity is commercial software and costs $20. You can use it for free, but you'll be prompted frequently to pay.  

A free alternative is [DevDocs](http://devdocs.io/), which is what I'm using now. Regardless, having a central repository of all your documentation sets is a good idea.  

### Install Postman
[Postman](https://www.getpostman.com/) is a desktop application that lets you test APIs and see detailed information about the response.  

Postman is really useful for testing your own APIs to make sure they deliver the desired response; but if you're looking to build an front-end application using a 3rd party API (like Twitch or Spotify), you're better off using a browser [extension](https://github.com/callumlocke/json-formatter) so you can traverse the JSON response in the console (e.g., `json.items.forEach(item => console.log(item))`).  

The Chocolatey package for Postman is not updated regularly and is lagging behind the latest release by a few months, so I recommend using the regular installer from the Postman website.  

### Install MongoDB
`choco install mongodb.install`  
`choco install mongodb`  

[MongoDB](https://www.mongodb.com/) is a NoSQL (non-relational) document store. If you use Mongo in your app, you'll want to use the [Mongoose](https://www.npmjs.com/package/mongoose) ODM. You'll install Mongoose as a dependency in your project using Yarn.  

You first need to create a database directory. The default is C:\data\db. You can create a directory anywhere, just pass the `--dbpath` flag after `mongod.exe` followed by the entire path of the directory (e.g., `.\mongod.exe --dbpath C:\path\to\my\database`).  

To start the MongoDB server, you need to run the `mongod` executable from PowerShell:  

1. `cd "\Program Files\MongoDB\Server\3.2\bin"`
2. `.\mongod.exe`

Now that the server is running, you can connect your app or a GUI client to it; or use the MongoDB shell with the `mongo` command.  

See the "Suggested System Tools" section to add MongoDB to your `PATH` so you can run `mongod` and `mongo` anywhere.  

Alternatives are CouchDB or Couchbase.  

Want a local, serverless database? Check out [LowDB](https://github.com/typicode/lowdb) which writes to a JSON file using Lodash methods. Slightly more advanced is Google's [LevelDB](https://github.com/Level/level), which is a simple key-value store that can accept JavaScript objects as values. Lastly, [NeDB](https://github.com/louischatriot/nedb) is a JavaScript-based database using a subset of the MongoDB API that can exist in-memory or in a persistent file.  

### Install MongoDB GUI
Two options:  

[Mongo Client](https://www.mongoclient.com/), which is a portable (no installation - easy removal) Electron Meteor desktop application. To update it, you have to delete the old version and download the new version from GitHub.  

[MongoDB Compass](https://www.mongodb.com/products/compass) is from MongoDB Inc. You'll be required to enter your email and phone number to download it. I think it's faster and easier to use than Mongo Client, but it really comes down to your preference for open source software, or software that requires you to give your personal contact information to use.  

### Install PostgreSQL
[PostgreSQL](https://www.postgresql.org/) is an open source relational database management system. It's actively maintained and has been in development since the 90's. I personally prefer it to MySQL, and it's the database of choice for Heroku.  

The PostgreSQL docs are incredibly robust, but I also recommend the website [PostgreSQL Tutorial](http://www.postgresqltutorial.com/) to help get you started.  

You'll want to use an ORM like [Sequelize](http://docs.sequelizejs.com/) in your project. Alternatives are Bookshelf, Waterline, or Objection.  

The Chocolatey PostgreSQL package has not been updated in years, so you have two options: installing the EnterpriseDB distribution (commercial) or the BigSQL distribution (open source).  

I wanted to like BigSQL as it's open source and comes with a nifty command line package manager (like NPM but for PostgreSQL stuff). I just couldn't get it to work on either Mac or Windows. So for that reason, I'm out.  

PostgreSQL Tutorial recommends the [EnterpriseDB](https://www.enterprisedb.com/downloads/postgres-postgresql-downloads#windows) installer. The instructions are [here](http://www.postgresqltutorial.com/install-postgresql/). I'd recommend initializing your database cluster in the default directory (`C:\Program Files\PostgreSQL\9.6\data`).  

To start your server:  

1. run `cd "\Program Files\PostgreSQL\9.6\bin"`
2. run `.\pg_ctl start -D ..\data`  

To stop your server:  

1. run `cd "\Program Files\PostgreSQL\9.6\bin"`
2. run `.\pg_ctl stop -D ..\data`  

See the "Suggested System Tools" section to add PostgreSQL to your `PATH` so you can run `pg_ctl` from anywhere.  

The EnterpriseDB installer will also install the latest version of pgAdmin, which is an open source PostgreSQL GUI client.  

Note that the EnterpriseDB installer will add a registry key to start PostgreSQL everytime you start Windows. Use a tool like Autoruns to remove it.  

If you're just looking to play around with a SQL database, I highly encourage you to try [SQLite](http://sqlite.org/). SQLite is serverless and requires no configuration - creating a database is as easy as making a text file. You can also use SQLite while you're developing your app and designing your schema, and easily change to PostgreSQL when you deploy.  

If you are deploying your app to Heroku, you'll want to use PostgreSQL as SQLite is stored in memory and will be wiped whenever Heroku restarts your dyno (once per day). You can read more about that [here](https://devcenter.heroku.com/articles/sqlite3) and [here](https://devcenter.heroku.com/articles/dynos#ephemeral-filesystem). Heroku also offers a managed PostgreSQL database-as-a-service so you can focus on writing JavaScript and not being a DBA.  

### Configure ESLint
[ESLint](http://eslint.org/) is a JavaScript linter that allows you to write custom rules, or download style guides from companies like Airbnb and Google. Linters don't just warn you that your code looks hideous; they can also warn you when you've written something illegal that won't run (a syntax error) or that you've declared a variable and never referenced it anywhere else (which is also handy when you've mistyped or renamed the name of a variable or function).  

I wrote a Gist on setting up ESLint [here](https://gist.github.com/adamelliotfields/a6e351873bc0409e1d25d617cbf17341). I encourage you to Read Airbnb's [style guide](https://github.com/airbnb/javascript/blob/master/README.md) and the ESLint docs to define your own rules.  

Alternatively, you can check out [StandardJS](https://standardjs.com/). StandardJS attempts to be a uniform style guide for JavaScript, like PSR (PHP Standards Recommendations). There's no configuration - it just works. Why don't I use it? I personally like using semicolons.  

### Install and configure VS Code
I recommend VS Code if you're just starting out. It offers the most features out of the box compared to Atom and Brackets, with a decent ecosystem of extensions (not as good as Atom or Sublime). The integrated terminal is outstanding, and you can choose between Command Prompt, PowerShell, or Bash for your shell.  

[Here](https://gist.github.com/adamelliotfields/9e92ff650600d87b2afc9483122de754) is a gist on getting VS Code set up. I also wrote a Gist on configuring Atom [here](https://gist.github.com/adamelliotfields/b9a4064ce0b584670dff4dbe535e93f9) and one for Sublime [here](https://gist.github.com/adamelliotfields/58b4b69741559ca3d89b44d121195258).  

### Suggested NPM Packages
[Here](https://gist.github.com/adamelliotfields/029e4f413473391cd0eda02145564b37) is a Gist of packages you should check out.  

### Suggested Chrome Extensions
[Here](https://gist.github.com/adamelliotfields/d8a6242dd668f9660c33ba9c41a23973) is a Gist of Chrome Extensions I use that are useful for web development.  

### Suggested System Tools
While not directly related to development, these are programs that can make your Windows life easier.  

[PuTTY](http://www.putty.org/)  
Use this to SSH into a virtual machine (e.g., Digital Ocean, Google Compute Engine).  

Install via Chocolatey:

```
choco install putty.install
choco install putty
```

[AquaSnap](http://www.nurgo-software.com/products/aquasnap)  
On macOS I use the Spectacle app to position my windows with hotkeys (have the browser on the left-half and the editor on the right-half). AquaSnap is free for personal use and offers the same functionality (hold down the Windows key and press the left or right arrow key). I find using hotkeys faster than using Windows built-in AeroSnap, which is activated by dragging the window with the mouse. Use the installer from the website.  

[Rapid Environment Editor](https://www.rapidee.com/en/about)  
This is an AWESOME tool! Rapid EE is a GUI to easily edit your `PATH`. The Chocolatey package appears to be actively updated, so feel free to install it that way: `choco install rapidee`  

Here's how to add PostgreSQL to your `PATH` so you can run `pg_ctl start` from anywhere:  

1. Open Rapid EE as Admin
2. Under User Variables, right click anywhere and select "Add Variable"
3. For Variable Name, enter "PGDATA" (variable type is "string")
4. Paste the path to your PostgreSQL data directory - default is `C:\Program Files\PostgreSQL\9.6\data`
5. Right click on `PATH=`
6. Select "Add Value"
7. Paste the path to your PostgreSQL bin folder - default is `C:\Program Files\PostgreSQL\9.6\bin`
8. Goto "File" and click "Save"
9. Open a new PowerShell window and run `pg_ctl start` to make sure it worked  

Other environmental variables you may want to add are `PGDATABASE` (the default database to connect to), `PGUSER` (the default user to connect as), and `PGPASSWORD` (the password for `PGUSER`). You can view the full list [here](https://www.postgresql.org/docs/9.6/static/libpq-envars.html).  

Use the same process for adding `C:\Program Files\MongoDB\Server\3.2\bin` to your `PATH`.  

[Registrar Registry Manager](http://www.resplendence.com/registrar)  
If you've ever had to modify or delete registry keys, you know how slow `regedit` can be. Registrar returns all results in seconds, so no more doing "find next" to look for the right key. Registrar is free for personal use. Use the installer from the website.  

[Autoruns](https://technet.microsoft.com/en-us/sysinternals/bb963902)  
Autoruns is a Windows Sysinternals program by Microsoft Azure CTO Mark Russinovich. It's a portable app (no installation) that shows every process scheduled to start when loading Windows. Use it to see what third-party programs are scheduled to run in the background, and also check for processes attached to previously uninstalled programs (and delete them). Install using Chocolately: `choco install autoruns` and run from PowerShell by running `autoruns`.  

[ScreenToGif](https://github.com/NickeManarin/ScreenToGif)  
By far the easiest way to record screen captures and convert to gif. Install using Chocolatey: `choco install screentogif`.  

[Greenshot](http://getgreenshot.org/)  
The best screenshot tool for Windows. Install using Chocolatey: `choco install greenshot`

[NetBalancer](https://netbalancer.com/)  
NetBalancer is a network monitoring program (and the best I've found) to see the bandwidth used by each program individually. For example, recently I noticed the Oculus Rift application had silently uploaded over 20GB and was not stopping (and was promptly uninstalled). NetBalancer is commercial software, and the unregistered version can only be used for network monitoring - the paid version unlocks features like controlling your network traffic with rules and priorities. Use the installer from the website.  

[HWiNFO](https://www.hwinfo.com/)  
HWiNFO is used to display system information like temperatures and fan speeds. HWiNFO is freeware and can be installed using Chocolatey:

```
choco install hwinfo.install
choco install hwinfo
```  

[Rainmeter](https://www.rainmeter.net/)  
Rainmeter is a desktop customization tool using skins made by the Rainmeter community. Skins can be simple widgets to display the weather, all the way up to complete desktop enhancement suites.  

I'm currently using the [NXT-OS](http://nxtos.com/) desktop suite, as well as [ModernGadgets](https://github.com/iamanai/ModernGadgets)  which displays CPU and GPU data from HWiNFO, as well as SSD and Network bandwidth.  

Install from the Rainmeter website.  
