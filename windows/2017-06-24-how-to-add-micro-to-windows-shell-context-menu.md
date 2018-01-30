# Add Micro to Windows Shell Context Menu
> :calendar: *June 24, 2017*

For making quick edits to a file, I really like the command line text editor [Micro](https://github.com/zyedidia/micro).

### Install Micro
Run `choco install micro`

### Edit the Registry
1. Run `regedit`
2. Click `HKEY_CLASSES_ROOT`
3. Click `*`
4. Right click `shell`, select `New Key`, and name it `Open with Micro`
5. Right click `Open with Micro`, select `New Key`, and name it `command`
6. Under the `command` key, right click `(Default)` and select `Modify`
7. Under `Value data`, enter: `C:\ProgramData\chocolatey\bin\micro.exe %1`

You should now be able to right click files in File Explorer and open them with Micro.
