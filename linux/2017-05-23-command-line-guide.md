# Command Line Guide
Being able to use a command line interface is a must-have skill for any JavaScript developer. You'll need to download dependencies from NPM, run a web server, database server, task runner, compilers, and push changes to a repository. There are also a ton of really cool CLI programs available on NPM to download, and creating your own CLI apps is super fun too.  

Just about everything you need to do can be done from the stock command line interfaces on macOS (Terminal) and Windows (Command Prompt, PowerShell, WSL). With that said, you can customize your environment to make your command line experience more enjoyable and productive.  

### POSIX
POSIX is a set of standards for maintaining compatibility between operating system APIs. macOS is POSIX certified and most Linux distributions are POSIX compliant (the major difference is that getting certified costs money). This is why you can switch from macOS to Ubuntu and the command line experience will be mostly the same.  

The Windows API, Win32, is not POSIX compliant. For example, to get to your root directory on Linux or macOS, you'd enter `cd /` and see `/` as your current working directory. Conversely, on Windows, the command is `CD\` and you'd see `C:\`. This is a trivial example, but the take-away is that POSIX filesystems and the methods to interact with them are completely different than Windows.  

A few examples of POSIX standards:

1. [Shell Language](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/V3_chap02.html#tag_18) - e.g., Bash
2. [Directory Structure](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap10.html#tag_10) - e.g., `/usr/local/bin`
3. [Built-in Utilities](http://pubs.opengroup.org/onlinepubs/9699919799/utilities/V3_chap01.html#tag_17_06) - e.g., `cd`, `touch`, `mkdir`
4. [Environment Variables](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap08.html#tag_08) - e.g., `$HOME`, `$PATH`

### Bash
The default shell on macOS and Ubuntu is Bash (Bourne-again SHell). When you open a new Terminal, it runs the binary `/bin/bash`. Bash is both a shell (an interactive operating system user interface) and a scripting language. macOS also ships with Z Shell (`zsh`), C Shell (`tcsh`), and Korn Shell (`ksh`).  

Using Bash, I recommend checking out the framework [Bash-it](https://github.com/Bash-it/bash-it), which provides an interface to download and install useful addons for your Bash shell.  

Bash-it addons are categorized as plugins, completions, and themes.  

**Bash-it Plugins:**  
Show: `bash-it show plugins`  
Enable: `bash-it enable plugin <plugin>`  
Disable: `bash-it disable plugin <plugin>`  

I'm using `git`, `hub`, `node`, `npm`, and `osx`.  

**Bash-it Completions:**  
Show: `bash-it show completions`  
Enable: `bash-it enable completion <completion>`  
Disable: `bash-it disable completion <completion>`  

I'm using `brew`, `git`, `hub`, `npm`, and `nvm`.  

**Bash-it Themes:**  
Bash-it ships with over 50 themes. Themes transform the display of your command prompt, and show useful information like if you have changed files in a Git repository that need to be committed. You can see screenshots of all Bash-it themes [here](https://github.com/Bash-it/bash-it/wiki/Themes).  

To change your theme, simply edit your `.bash-profile` in your home directory (`~/`). Look for the line with `export BASH_IT_THEME='bobby'` and change `'bobby'` to whatever theme you like.  

### Fish
[Fish](https://fishshell.com) is an alternative command line shell that is both powerful and easy to use. Fish provides features like syntax highlighting, autocompletion, and even a browser-based tool for configuration.  

Installing Fish on macOS is a breeze thanks to Homebrew. Simply run `brew install fish`. You can enter the Fish shell by running `fish`, or you can configure Terminal to use Fish by default by going to Terminal > Preferences > General > "Shells open with" and entering `/usr/local/bin/fish`.  

I recommend using the [oh-my-fish](https://github.com/oh-my-fish/oh-my-fish) framework which is a package manager for Fish. OMF packages can be plugins or themes.  

I'm using the `brew`, `hub`, `nvm`, and `osx` plugins and the `bobthefish` theme. Note that in order to use a Powerline theme like `bobthefish`, you need to install a Powerline font and also set it as your Terminal's default font. I'm using [Droid Sans Mono for Powerline](https://github.com/ryanoasis/powerline-extra-symbols/tree/master/patched-fonts).  

You can search for plugins or themes using `omf search <name>`. Likewise, you can install packages using `omf install <name>`.  

It's worth noting that Fish's scripting language is different than Bash, and Fish also handles your `PATH` differently than Bash (amongst other differences). I personally think one should be comfortable with Bash first, before learning an alternative. Just like how you should learn JavaScript before learning Coffeescript.  

If Fish doesn't sound like your cup of tea, and you'd like something more powerful than Bash, you can also try [zsh](http://zsh.sourceforge.net). Zsh is generally considered a more advanced shell, and it can be enhanced using the incredibly popular (50k+ stars) [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh) framework.  

### PowerShell
If you're using Windows, you have two shells installed by default - Command Prompt and PowerShell. This [article](https://www.howtogeek.com/163127/how-powershell-differs-from-the-windows-command-prompt) from How-To Geek gives a nice introduction to how the two differ.  

I'm personally using PowerShell, and have customized it using [posh-git](https://github.com/dahlbyk/posh-git) and [PSReadline](https://github.com/lzybkr/PSReadLine).  

Alternatively, if you want a native Linux command line experience on Windows, you can enable the Windows Subsystem for Linux (WSL) and install Bash on Ubuntu on Windows. This [article](https://www.howtogeek.com/249966/how-to-install-and-use-the-linux-bash-shell-on-windows-10) also from How-To Geek explains the steps.  

There are other options like [Git Bash](https://git-for-windows.github.io) and [Cygwin](https://www.cygwin.com), but I do not use them.  

### Terminal Emulators
Terminal emulators provide an interface to the operating system in conjunction with a shell. They are called terminal emulators because they are programs that emulate physical hardware (a computer terminal).  

The default terminal emulator on macOS is `Terminal.app`. On Windows, there are the `cmd.exe` and `powershell.exe` applications.  

Once you've determined which shell to use, you may want to try a third-party terminal emulator. I'm personally using [Hyper](https://hyper.is) on both macOS and Windows. Popular alternatives are [iTerm2](https://www.iterm2.com) for macOS and [ConEmu](https://conemu.github.io) for Windows.  

Hyper also has a package manager, [hpm-cli](https://www.npmjs.com/package/hpm-cli), available on NPM, to make installing and managing plugins simple. I'm using the [hyperline](https://www.npmjs.com/package/hyperline) plugin, which shows system information like available memory, CPU usage, and network bandwidth.  
