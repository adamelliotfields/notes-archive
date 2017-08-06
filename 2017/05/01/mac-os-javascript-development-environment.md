# macOS JavaScript Development Environment
This is my development setup on my Macs. I have been doing a lot of work on Windows lately, but I still think Macs "just work".  

### Install Xcode Command Line Tools
Xcode Command Line Tools add a bunch of tools and utilities to the macOS Terminal. You do not need to install Xcode itself, though.  

`xcode-select --install`  

### Install Homebrew
Homebrew is a package manager for macOS, similar to APT on Linux. There are thousands of packages available, and you can browse them [here](http://brewformulas.org/). Homebrew packages are installed to `/usr/local/Cellar` and are symlinked to `/usr/local`.  

`/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`  

### Install Cakebrew
Cakebrew is a GUI for Homebrew. View your installed packages and update them when necessary.  

Download [here](https://www.cakebrew.com/files/cakebrew-1.2.3.dmg).  

### Install Git
Xcode Command Line Tools will install Git; however, use Homebrew to keep your Git installation up to date.  

`brew install git`  

You should also install TJ Holowaychuk's [Git Extras](https://github.com/tj/git-extras). This will give you access to commands like `git undo` to undo your last commit. Install using Homebrew:  

`brew install git-extras`  

Finally, you should install [Hub](https://hub.github.com/) which further extends Git, by allowing you to interface with GitHub from the command line. You can do things like create a GitHub repository and easily clone a repository:  

`brew install hub`  

### Configure Git
Read my Gist [here](https://gist.github.com/adamelliotfields/60415694ca2a511dcaeb4e3be78017b4).  

### Install Git Kraken
[Git Kraken](https://www.gitkraken.com/) is a GUI for Git that is better than Github Desktop in my opinion.  

Git Kraken has a neat feature that watches an entire folder of Git repositories (all my repos are in my `GitHub` folder, some people use a folder named `Projects`; just don't use the folder called `Dropbox`). I can simply see which repositories are behind, and pull the repo I plan to work on.  

### Node Version Management
Instead of installing Node using the installer from NodeJS.org or through Homebrew, I recommend using a version management tool. There are two: [NVM](https://github.com/creationix/nvm) and [n](https://github.com/tj/n).  

I personally use NVM. I use NVM on Windows, so the `nvm install` and `nvm use` commands are the same across platforms. With that said, n is still a great tool and was originally made by TJ Holowaychuck who also made Express and Koa (amongst lots of other things).  

NVM has some cool features like automatically re-installing your global NPM packages when you install a new version of Node. You can even create a `default-packages` file listing the NPM packages you want to install every time you install a version of Node.  

To install NVM:  

1. Make sure you're in your home directory: `cd ~`
2. Clone the repo into the .nvm folder: `git clone https://github.com/creationix/nvm.git .nvm`
3. Check out the latest version: `git checkout v0.33.2`
4. Open your `.bash_profile` in Nano: `nano .bash_profile`
5. Paste `export NVM_DIR="$HOME/.nvm"`
6. Paste `[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"`
7. Enter `CTRL-x` followed by `y` and `RETURN` to save and quit Nano
8. Source your profile: `source .bash_profile`

To install Node:  

`nvm install node` installs the latest version of Node. `npm use node` will use that version.  

You can install specific versions like this: `nvm install 6.10.2` and `nvm use 6.10.2`.  

### Install Node
If you do not want to use Node Version Management, then simply install Node via Homebrew.    

`brew install node`  

### Install Yarn
I've been using Yarn to manage project dependencies. I encourage you to listen to this episode of [JavaScript Air](https://javascriptair.com/episodes/2016-11-02-bonus/) to learn about Yarn from the people who made it.  

If you installed Node using NVM, do not install Yarn with Homebrew. Yarn requires Node to be installed, and Homebrew will not know that you installed Node externally. Because of this, I recommend using NPM:  

`npm install --global yarn`  

If you aren't using NVM, you may install Yarn using Homebrew:  

`brew install yarn`  

### Install Dash
[Dash](https://kapeli.com/dash) is optional, since it costs $25. You can use it for free; however, it will frequently block you from reading for 8 seconds at a time until you pay for it.  

Dash has integrations with Atom as well as the desktop search tool [Alfred](https://www.alfredapp.com/).  

A free alternative is [DevDocs](http://devdocs.io/), which is what I'm using.  

### Install Postman
[Postman](https://www.getpostman.com/) is a desktop application that lets you test APIs and see detailed information about the response.  

Postman is really useful for testing your own APIs to make sure they deliver the desired response; but if you're looking to build an front-end application using a 3rd party API (like Twitch or Spotify), you're better off using a browser [extension](https://github.com/callumlocke/json-formatter) so you can traverse the JSON response in the console (e.g., `json.items.forEach(item => console.log(item))`).  

Download it [here](https://www.getpostman.com/apps).  

### Install Database Servers
While I do just about everything in Terminal, Macs have some slick tools that make managing database servers a breeze.  

When deploying your app, chances are you're going to use a database-as-a-service like PostgreSQL on Heroku, or MongoDB on mLab. These services take care of database administration, so you can focus on hooking them up to your app and using them.  

For PostgreSQL, you cannot do any better than [Postgres.app](http://postgresapp.com/). Just open the app and start the server. For MongoDB, check out [MongoDB.app](http://gcollazo.github.io/mongodbapp/).  

### Install Database GUIs
Nobody likes viewing large SQL tables in Terminal. [pgAdmin](https://www.pgadmin.org) is an open-source GUI for PostgreSQL. If you spend a lot of time in PostgreSQL and you're on a Mac, check out [Postico](https://eggerapps.at/postico/). Postico costs $40, but it's definitely the most user friendly PostgreSQL GUI I've seen.  

For MongoDB, I recommend [Mongoclient](https://www.mongoclient.com/).  

### Configure ESLint
[ESLint](http://eslint.org/) is a JavaScript linter that allows you to write custom rules, or download style guides from companies like Airbnb and Google. Linters don't just warn you that your code looks hideous; they can also warn you when you've written something illegal that won't run (a syntax error) or that you've declared a variable and never referenced it anywhere else (which is also handy when you've mistyped or renamed the name of a variable or function).  

I wrote a Gist on setting up ESLint [here](https://gist.github.com/adamelliotfields/a6e351873bc0409e1d25d617cbf17341).  

### Install a Text Editor
I've used Atom, VS Code, Brackets, Sublime, and Webstorm.  

Sublime is the best editor, in my opinion. It loads instantly and doesn't choke on large files. Sublime has an unlimited free tree, but if you do use Sublime daily, you should pay for it. I wrote a Gist on setting up Sublime [here](https://gist.github.com/adamelliotfields/58b4b69741559ca3d89b44d121195258).  

I personally recommend VS Code if you're starting out as it works the best out of the box. I wrote a Gist on setting up VS Code [here](https://gist.github.com/adamelliotfields/9e92ff650600d87b2afc9483122de754), and another one for Atom [here](https://gist.github.com/adamelliotfields/b9a4064ce0b584670dff4dbe535e93f9).  

Brackets is a good tool if you're doing a lot of web design work. It has a built-in dev server with live reloading as well as native support for Sass and Less.  

Webstorm should not be your first editor. Only upgrade to Webstorm once you've tried other editors and either had issues (i.e., crashes, deprecated plugins) or simply needed an integrated feature only available in Webstorm.  

### Configure Your Command Line
Read my Gist [here](https://gist.github.com/adamelliotfields/c2cf80995419266361a35cbd6274e0a8).  

### Install Micro
[Micro](https://github.com/zyedidia/micro) is a terminal-based text editor intended to be an upgrade from Nano. Sometimes you need to make a quick edit to a file from the command line, and Micro is more powerful and easier to use than Nano.

`brew install micro`  

### Configure Bash Profile
Your `.bash_profile` is located in your home (`~/)` directory and is loaded every time you open a new shell.  

```
export PATH=/usr/local/bin:/usr/bin:/bin:/usr/local/sbin:/usr/sbin:/sbin
```

The first line is my `PATH`, which is an environmental variable that tells the shell (Bash) where to search for executable files. The order is important. I'm telling Bash to look in `/usr/local/bin` first.  

Remember when you installed Xcode Command Line Tools, which installed Git? It installed Git to `/usr/bin`. Since I want to use the Homebrew version in `/usr/local/bin`, I want `/usr/local/bin` to appear first. Bash will execute the first binary it finds, otherwise it will continue searching down the list of directories in the `PATH`.  

Another example is MongoDB.app. The executables are in `/Applications/MongoDB.app/Contents/Resources/Vendor/mongodb`. Note that `/Applications` refers to the root Applications directory - not the User applications directory in `~/Applications`. If you want access to MongoDB's command line tools, you'll have to add `/Applications/MongoDB.app/Contents/Resources/Vendor/mongodb` to your `PATH`. Simply add this line after the first `export PATH` declaration:  

`export PATH=$PATH:/Applications/MongoDB.app/Contents/Resources/Vendor/mongodb`  

Any time you make changes to `.bash_profile`, you need to *source* those changes by running `source ~/.bash_profile`.  

You can always see what your `PATH` is by running `echo $PATH` in Terminal.  

### Suggested NPM Packages
[Here](https://gist.github.com/adamelliotfields/029e4f413473391cd0eda02145564b37) is a Gist of packages you should check out.  

### Suggested Chrome Extensions
[Here](https://gist.github.com/adamelliotfields/d8a6242dd668f9660c33ba9c41a23973) is a Gist of Chrome Extensions I use that are useful for web development.  

### Suggested Tools
[Spectacle](https://www.spectacleapp.com/)  
Allows you to quickly resize and position windows using hotkeys. I could not live without it.  
