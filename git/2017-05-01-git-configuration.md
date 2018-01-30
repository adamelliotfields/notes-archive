# Git Configuration
> :calendar: *May 1, 2017*

Your global `.gitconfig` file should be placed in your home directory (`/Users/<username>` on macOS or `C:\Users\<username>` on Windows). You can also have a `.gitconfig` per project, as well as a `.gitattributes` file, but I prefer to just use global settings.  

### Line Endings
Windows uses CRLF (`\r\n`) by default. This differs from Unix-like operating systems (macOS, Linux), which use LF (`\n`). You can read more about this [here](https://help.github.com/articles/dealing-with-line-endings/#platform-all) and [here](http://adaptivepatchwork.com/2012/03/01/mind-the-end-of-your-line/).  

Why is this a big deal? Because GitHub compares 2 files (the old one and the new one). If your old file had `\n` at the end of every line, and your new file has `\r\n`, Git will assume you changed every line in the file.  

I'm personally using `core.autocrlf input` on both Windows and macOS. On Windows, when I do a `git add`, I get this lovely message:  

```
warning: CRLF will be replaced by LF in README.md.
The file will have its original line endings in your working directory.
```

...which is exactly what I want to happen.  

Most guides will recommend using `core.autocrlf true`, which will convert CRLF to LF in the repo, but leave CRLF in the working directory. But there's a catch: if you are already using LF line endings in your editor on Windows, it will convert them to CRLF in the repo, which is the exact opposite of what you want.  

### Editor
On Windows I use `notepad` and on macOS I use `nano`.

You can also avoid this entirely by just running `git commit -m "I'm a commit message"` (which is what you should be doing all the time).  

### Hub
[Hub](https://hub.github.com) is an extension to Git by the GitHub team, allowing you to interface with GitHub from the command line. The `hub.protocol https` setting tells Git to connect to GitHub via `https` instead of `ssh`. If you don't have `ssh` set up, this is the setting to use. If you don't have Hub installed, you don't need this setting.  


### `.gitconfig`
```
[user]
  name = Your Name
  email = your@email.address
[core]
  autocrlf = input
  editor = nano -w
[hub]
  protocol = https
```  
