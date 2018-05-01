---
layout: page
title: Web Scraping Part I: Command Line Basics
description: Tutorial on using the command line 
---


> This tutorial is written for Mac users. 

# Using the Command Line

The easiest method for writing and running python scripts (in my opinion) is to edit your python scripts in a text editor and run them using the command line. I use Komodo Edit as my text editor, but there are plenty of other options. It doesn't matter which you use, but you do need to use an editor that works on plain text, not a word processor such as Microsoft Word. 

Before we get to the python-specific part, it's useful to go over a few command line basics. You can open the command line by spotlight searching for ''Terminal'', or you can find it in Applications > Utilities. 

The command line allows you to do a whole bunch of things that you already do on your computer, but instead of clicking with the mouse, opening windows, etc. everything will be done by issuing commands. 

### Some Terminology
When you open the **terminal**, you'll see the **console**, the **command line**, and the **prompt**:
* **console**: everything above the command line - this is where output will be written if you issue commands or if you run a python script and have a "print" command in your script.
* **prompt**: beginning of the command line - follows the `$`. **Note you do not need to type the `$` when issuing a command** - this is just used to signify that the code being referenced is issued at the command line.
* **command line**: line where you type your command 

### Useful Commands
When you open the terminal, the first thing you'll want to do is figure out where you are. This is your "current working directory" and it is akin to the folder that you are currently in if you opened the finder and navigated to a certain folder. 

#### Print working directory (i.e. figure out where you are) - `pwd`:
To see where you are, type: 
```bash
$ pwd
```
and press enter. A path will print to the console which will indicate the folder that you are currently in. This is called the "current working directory" or just "working directory".

#### change directory - `cd`:
To move to another folder (i.e. change your working directory) use the command `cd`. Let's say I have some python files that I want to run stored in the folder /Users/marisacarlos/Dropbox/Cornell/Python_Tutorial. If I issue the command:
```bash
$ cd /Users/marisacarlos/Dropbox/Cornell/Python_Tutorial
```
it will take me to this folder.

>**Note 1**: If any of the folders or files in your path have spaces in them, you'll need to enclose it in quotes.

>**Note 2**: The "/" at the beginning of the path is important - it signifies the root directory. If I typed `$ cd Users/marisacarlos/Dropbox/Cornell/Python_Tutorial`
it would look for a folder called `Users` in my working directory instead of the folder `Users` in my root directory (where it actually is). 

#### List the contents of a folder - `ls`:
To see the contents of a folder use the command `ls`. Typing `$ ls` will show a list of files in your working directory. If you specify a path after `ls` (e.g. `ls /Users/marisacarlos/Dropbox/Cornell`, it will show a list of files in the folder path you specify. 

#### Open a file - `open`':
If you want to open a file without double clicking on the file in its folder, you can use the `open` command. For example, if my current directory contained the file workbook.xlsx, I could open it by typing:
```bash
open workbook.xlsx
```

#### Removing files using `rm`:
Issuing commands at the command line can be dangerous because you have the power to make permanent changes to your computer. An example of this is the command `rm` which removes files. `rm` is different from right-clicking on a file and moving it to the trash because `rm` deletes the file permanently and does not place it in the trash folder. For this reason I suggest two things:

1. Use Dropbox or Box or some other cloud storage to backup all your files continuously. I'm assuming you're doing this already, but if not you should because this is the second most important insurance policy you'll have right now (after health insurance). If you're really risk averse I'd suggest backing up to a physical external hard drive every few months or so. 
2. Add `alias rm="rm -i"` to the file ~/.bash_profile. Your bash profile is basically a list of commands that run in the background whenever you open your terminal. The command `alias rm="rm -i"` tells your computer to interpret the command `rm` as `rm -i`. The option `-i` requires you to enter confirmation before it is acutally deleted. So, if you add this to your bash profile, thn whenever you issue the command `$ rm file.txt` a message will print to the console that says `remove file.txt?`. If you type y (or ye or yes) and push enter it will remove the file; type anything else and the file won't be removed. 

   **To add this to your bash profile do the following:**
   
   1.  Type `$ nano ~/.bash_profile`
   2. Use the down arrow to navigate to the last line of the file add a new line containing `alias rm="rm -i"`
   3. Save the file by typing `ctrl + o` (control followed by the "o" letter key) and then **enter**
   4. Exit nano (the text editor) by typing `ctrl + x`
   5. Activate the changes by typing `$ source ~/.bash_profile` (you only need to do this once - i.e. you don't need to do it every time you open the terminal)
   
   >**note**: You can also change what your command prompt name is by adding the following line to your bash profile: `export PS1="whatevernameyouwant$ "` - activate the bash profile and see how the prompt changes.

### Other Useful Things
#### Path shortcuts:
`../` can be used to refer to the directory *above* the one you are currently in. For example, if your current working directory is: 
```bash
/Users/marisacarlos/Dropbox
```
then `../` will correspond to the path: 
```bash
/Users/marisacarlos
```
and `../../` will correspond to the path: 
```bash
/Users
```
and so on.

Don't want to type the whole path/file name? The **tab** key on your keyboard will automatically fill in the name (up to the point where it needs more information). 

Use the **up arrow** to see commands you previously issued.


#### Command options:
Most commands have options. For example, if you issue the command `ls -a` the option `-a` tells your computer to list all files, include those that begin with a dot **(.)**. To see all the options available for the command ls, type `$ man ls`. Use enter or the trackpad/mouse to scroll through and type `q` to exit and return to the command prompt.

##### Useful `ls` options:
* `-c`: sort by date/time last modified
* `-l`: list files in long format instead of multiple columns (easier to read sometimes)
* `-G`: color-code the items (makes it easy to see which are folders and which are files)

  > **Note**: `$ ls -a -l` is equivalent to `$ ls -al` and `$ ls -la`

