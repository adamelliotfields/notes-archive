# Codecademy Command Line Glossary
> :calendar: *February 12, 2017*

The command line is a text interface for your computer. It's a program that takes in commands, which it passes on to the computer's operating system to run.

### BASH

Bash is a Unix shell and command line language run by Apple Terminal. Bash stands for "Bourne Again SHell" and is an open source replacement for the original Bourne Shell. The `bash` command will start a new session inside the existing session.

### CAT

`cat` is short for concatenate and prints the contents of a file to the terminal. `cat` also accepts multiple files as arguments and displays their contents one after the other.

```sh
$ cat filename.txt
```

### CD

`cd` takes a directory name as an argument, and switches into that directory.

```sh
$ cd Desktop
```

To navigate directly to a directory, use `cd` with the directory's path as an argument.

```sh
$ cd ~/Desktop
```

To move up one directory, use `cd ..`.

### CLEAR

`clear` brings the prompt to the top of the screen.

### CP

`cp` creates a copy of a file. `cp` takes 2 arguments: the file name and the name of the new file or directory.

```sh
$ cp filename.txt desktop
```

`cp -r` recursively creates a copy of a directory and all its contents.

```sh
$ cp -R Projects desktop
```

### ECHO

`echo` displays the arguments sent to it. Useful for displaying the values of environment variables.

```sh
$ echo $PATH
```

### ENV

The `env` command stands for "environment", and returns a list of the environment variables for the current user.

### EXIT

`exit` ends the current terminal session. Alternatively, exit will revert to the original user if you switched users during the session.

### EXPORT

`export` makes the variable to be available to all child sessions initiated from the session you are in. This is a way to make the variable persist across programs.

```sh
$ export PATH=/Users/adamfields:$PATH
```

### FIND

`find directory -name` looks for files.

```sh
find ~ -name app.js
```

### GREP

`grep` stands for "global regular expression print". It searches files for lines that match a pattern and returns the results. It is case sensitive.

```sh
$ grep "function" app.js
```

`grep -i` enables the command to be case insensitive.

```sh
$ grep -i "FUNCTION" app.js
```

`grep -n` shows line numbers next to each result

```sh
$ grep -n "function" app.js
```

`grep -v` shows all lines that DON'T contain the pattern.

```sh
$ grep -v "function" app.js
```

`grep -R` searches all files in a directory and outputs filenames and lines containing matched results. `-R` stands for "recursive".

```sh
$ grep -R app /Users/adamfields/Projects
```

`grep -Rl` searches all files in a directory and outputs only filenames with matched results. `-R` stands for "recursive" and `l` stands for "files with matches".

```sh
$ grep -R app /Users/adamfields/Projects
```

### HOME

The `HOME` variable is an environment variable that displays the path of the home directory.

```sh
$ echo $HOME
```

The home directory on OSX is `~` or `/Users/adamfields`

### LESS

`less` is a terminal pager used to display the contents of a text file.

```sh
$ less filename.txt
```

### LOCATE

`locate` searches an indexed database for a specific file. The default database is in `/var/db/locate.database`.

To update the database, run `sudo /usr/libexec/locate.updatedb`.

To find a folder, type `locate foldername | grep /foldername$`.

### LS

`ls` lists all files and directories in the working directory.

`ls -a` lists all contents in the working directory, including hidden files and directories.

`ls -l` lists all contents of a directory in long format.

`ls -t` orders files and directories by the time they were last modified.

### MKDIR

`mkdir` takes in a directory name as an argument, and then creates a new directory in the current working directory.

```sh
$ mkdir Projects
```

`mkdir -p` is used to create nested directories.

```sh
$ mkdir -p Projects/bash
```

### MV

To move a file into a directory, use `mv` with the source file as the first argument and the destination directory as the second argument. You can also rename files by "moving" them to a new file name.

```sh
$ mv filename.txt directory
```

### NANO

`nano` is a command line text editor. It works just like a desktop text editor like TextEdit, except that it is accessible from the the command line and only accepts keyboard input. Nano is an open-source emulator of Pico.

```sh
$ nano filename.txt
```

### Ownership and Permissions

`chown` changes the ownership of a file.

```sh
$ chown adamfields filename.txt
```

`chown -R` recursively changes the ownership of a directory.

```sh
$ chown adamfields ~/Projects
```

`chown` can also change the owner and group owner of a file using the `chown owner:group filename` syntax.

```sh
$ chown adamfields:staff filename.txt
```

`chgrp` changes the group owner of a file. `chgrp -R` recursively changes the group of a directory and its contents.

```sh
$ chgrp staff filename.txt
```

`chmod` changes the permissions of a file using the `chmod options permissions filename` syntax. Permissions use the UGO (User, Group, Other) and RWX (Read, Write, Execute) syntax. `=` sets the permissions, `+` adds a new permission, and `-` removes a permission. The `-R` option may be given to recursively change the permissions of a directory.

```sh
$ chmod u=rwx,g=rx,o=r filename.txt
```

### PATH

`PATH` is an environment variable that stores a list of directories separated by a colon. Each directory contains scripts for the command line to execute. `PATH` lists which directories contain scripts.

```sh
$ echo $PATH
```

`~/.bash_profile` is the name of file used to store environment settings. It is commonly called the "bash profile". When a session starts, it will load the contents of the bash profile before executing commands.

```sh
$ nano ~/.bash_profile
```

The `alias` command allows you to create keyboard shortcuts, or aliases, for commonly used commands in the bash profile.

```sh
alias pd="pwd"
```

`source` activates the changes in the bash profile for the current session. Instead of closing the terminal and needing to start a new session, `source` makes the changes available right away in the session we are in.

```sh
$ source ~/.bash_profile
```

### Processes

`top` is a program to show the currently active processes, similar to Activity Monitor.

`ps` shows the process status in the terminal. On its own, `ps` just shows what's running in the current session. `ps aux` will show all processes.

`ps aux | grep` will pipe the output of `ps aux` to `grep` and filter using the process name.

```sh
$ ps aux | grep firefox
```

`kill` takes 2 arguments: the signal and the PID. The default signal is `-SIGTERM` which stops the process normally. `-SIGKILL` will immediately terminate the process. `TERM` asks the process to stop; `KILL` forces the process to stop. To see a list of all signals, type `kill -l`.

```sh
$ kill -SIGKILL 20508
```

`killall` can be used to kill all processes with the same name. Alternatively, you can use `killall` when you do not know the PID.

```sh
$ killall -SIGKILL firefox
```

To open a program in the background, follow it with `&`. To bring that program to the foreground, type `fg`.

`jobs` will show all currently running jobs (processes in the current session only).

`CTRL-Z` will `STOP` the current job.

`CTRL-C` will `TERM` the current job.

### PWD

`pwd` prints the name of the working directory.

### Redirection

`>` takes the standard output of the command on the left, and redirects it to the file on the right.

```sh
$ cat file1.txt > file2.txt
```

`>>` takes the standard output of the command on the left and appends (adds) it to the file on the right.

```sh
$ cat file1.txt >> file2.txt
```

`<` takes the standard input from the file on the right and inputs it into the program on the left.

```sh
$ cat < filename.txt
```

`|` takes the standard output of the command on the left, and pipes it as standard input to the command on the right.

```sh
$ ps aux | grep -i firefox
```

### RM

`rm` deletes files.

```sh
$ rm filename.txt
```

`rm -r` recursively deletes a directory and all of its child directories.

```sh
$ rm -r Projects
```

### SED

`sed` stands for "stream editor". It accepts standard input and modifies it based on an expression, before displaying it as output data. In this example, `sed` will substitute "Hell" for "Heaven".

```sh
$ echo "Hello" | sed 's/Hell/Heaven/'
```

### SORT

`sort` takes a filename or standard input and orders each line alphabetically, printing it to standard output.

```sh
$ sort list.txt
```

### Standard I/O and Error

`stdin` is information inputted into the terminal through the keyboard or input device.

`stdout` is the information outputted after a process is run.

`stderr` is an error message outputted by a failed process.

### TOUCH

`touch` creates a new file inside the working directory. It takes in a file name as an argument, and then creates a new empty file in the current working directory.

```sh
$ touch filename.txt
```

### UNIQ

`uniq`, short for "unique", takes a filename or standard input and prints out every line, removing any exact duplicates.

```sh
$ uniq filename.txt
```

### Users

`adduser` creates a new user, home directory, and group. You need super user access to create a new user, and you'll also need to asign a password to the new user.

```sh
$ adduser adam
```

`su` allows you to switch users.

```sh
$ su adam
```

`sudo` allows you to perform a command as the super user. `sudo !!` runs the previous command as the super user.

`whoami` prints the name of the current user.

### WHICH

`which` prints the location of a program.

```sh
$ which node
```

### Wildcard

The wildcard `*` selects all of the files in the current directory. 

```sh
$ cp * Projects
```

Here, `a*.js` selects all files in the working directory starting with "a" and ending with ".js", and copies them to Projects.

```sh
$ cp a*.js Projects
```
