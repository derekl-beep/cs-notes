# Administrator commands

## `sudo`

The `sudo` prefix command means this command will temporarily be executed with system administrator permissions. (The `su` part comes from `superuser`, which means system administrator. Other terms for this are `root user` or simply `administrator`.) Such commands are potentially dangerous because they can take control of your system. 

# Common commands

## `man`

The  `man`  command ("manual") shows help information for other commands. For example,  `man man`  will display the help information for  `man`  itself. To quit the help viewer screen, press the  `q`  key.

## `pwd`

The `pwd` command, "print working directory," will display the full name of the path you are in currently. This is mainly useful if you are using a terminal that doesn't already show that information at the command prompt.

## `ls`

The `ls` command lists directory contents. You can use it to list the current directory's contents, or you can specify another directory as an argument. You can also see a long-format listing including modification dates and hidden files, typing:

`ls -hal`

## `cd`

The `cd` ("change directory") command will let you move around the file system. You can specify a directory or type  `cd ..`  (with two dots) to go up one directory. As a shortcut,  `cd ~`  will take you directly to your user's home directory. On AWS Cloud9, you would normally want to use  `cd ~/environment`  instead, to arrive at the same directory that is shown in the graphical file list.

Usually, your terminal will support  **tab completion**, which means that if you are typing a path you can press `Tab` partway through typing and automatically have your command finished. This is lets you avoid having to laboriously type out long filenames. Just type the first few letters and press `Tab`.


# File management commands

These commands can create or delete files, so be careful before you try to use any of them! We just want you to be aware of what they do. You can read the instructions for each one with the  **man**  command, for example:  **man mv** will tell you all the details about the  **mv**  command.

## `cp`

The `cp` command will copy a file.

## `mkdir`

The `mkdir` command will make a new sub-directory.

## `mv`

The `mv` command will move or rename a file.

## `rm`

The `rm` command will "remove" or delete a file. Be very careful! 

> Written with [StackEdit](https://stackedit.io/).
