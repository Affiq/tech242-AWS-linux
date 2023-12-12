# Linux Basics


## General
Linux makes use of some keyboard shortcuts. These include:
* Tab - autocomplete file/directory name
* Shift + Insert - paste into CLI.
* Tilde ~ represents home directory
* .. represents parent directory
* . represents current directory

Linux also makes uses of a BASH - a Bourne Again Shell. Further shells can be displayed using ```/cat etc/shells```.

Linux also determines file types by contents rather than file extension name.

## Important Directories
* Home Directory - the directory which the user enters upon connecting the VM. This is referred to as a User's Home Directory, which contains all the users file, and can be referenced using ~
* Root Directory - this directory contains important files gained from the AMI, and is typically the parent parent of the Home Directory, and can be referenced using /

## Admin Privileges
* ```Sudo``` Perform a command as a superuser
* ```Sudo su``` Switch to a superuser

## CURL
* ```CURL <target-URL> --output <targetfile>```

## Navigation
Linux navigation uses navigation commands similar to the Git BASH terminal. These include the following:

* ```cd <directory/file>``` Change Directory to given path
  * ```cd ..``` Changes to parent directory
  * ```cd ~``` Changes to home directory
  * ```cd /``` Changes to root directory
* ```whoami``` Used to identify the current user logged in
* ```pwd``` Print Working Directory
  * ```pwd -a``` Print all the information about the working directory
* ```ls``` Lists files.
  * ```ls -l``` Lists Long - shows additional info such as RWX permissions
  * ```ls -o``` Lists hidden file
* ```Tree``` Shows Tree structure of directory.
* ```mv <target> <destination>``` Move a file/directory to a destination
* ```file <targetfile>``` Gives detail of file type`
* ```history``` History of executed commands
* ```!num``` Repeat a command in the history stack
* ```head -l <filename>``` Shows Head (1st line) of file
* ```tail -l <filename>``` Shows Tail (last line) of file
* ```nl <filename>``` Numbered Lines display of text file
* ```cat <filename> | grep <pattern> ``` Searches for pattern inside the file

  
## Creatings, Writing and Deleting Files
* ```mkdir <dirname>``` Make Directory 
* ```touch <filename>``` Make new file
* ```mv <target> <newtargetname>``` Used to rename a file.
* ```rm <filename>``` Remove file
* ```rmdir <directoryname>``` Remove directory
* ```cp <filename>``` Copies filename
* ```nano <filename>``` Opens up a text editor for a file
  
  
## Installation
* ```sudo apt install <packagename>``` Download as superuser

