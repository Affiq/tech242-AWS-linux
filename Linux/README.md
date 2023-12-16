# Linux Basics

- [Linux Basics](#linux-basics)
  - [Goals:](#goals)
  - [General](#general)
  - [Important Directories](#important-directories)
  - [Admin Privileges](#admin-privileges)
  - [CURL](#curl)
  - [Navigation](#navigation)
    - [Changing directories](#changing-directories)
    - [Print Working Directory](#print-working-directory)
    - [List File Methods](#list-file-methods)
    - [Read File Methods](#read-file-methods)
    - [Command History](#command-history)
    - [File Management](#file-management)
    - [Directory Management](#directory-management)
    - [Package Management](#package-management)


## Goals:
We would like to learn about important directories in Linux, possible shortcuts, the use of root privileges, basic navigation commands, file/directory creation and deleting, as well as other foundational commands.

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
* * ```whoami``` Used to identify the current user logged in


## CURL
* ```CURL <target-URL> --output <targetfile>```

## Navigation
Linux navigation uses navigation commands similar to the Git BASH terminal. These include the following:

### Changing directories
* ```cd <directory/file>``` Change Directory to given path
  * ```cd ..``` Changes to parent directory
  * ```cd ~``` Changes to home directory
  * ```cd /``` Changes to root directory
  
### Print Working Directory
* ```pwd``` Print Working Directory
  * ```pwd -a``` Print all the information about the working directory

### List File Methods
* ```ls``` Lists files.
  * ```ls -l``` Lists Long - shows additional info such as RWX permissions
  * ```ls -o``` Lists hidden file
* ```Tree``` Shows Tree structure of directory.

### Read File Methods
* ```head -l <filename>``` Shows Head (1st line) of file
* ```tail -l <filename>``` Shows Tail (last line) of file
* ```nl <filename>``` Numbered Lines display of text file
* ```cat <filename> | grep <pattern> ``` Searches for pattern inside the file

### Command History
* ```history``` History of executed commands
* ```!num``` Repeat a command in the history stack 

### File Management
* ```touch <filename>``` Make new file
* ```nano <filename>``` Opens up a text editor for a file
* ```file <targetfile>``` Gives detail of file type`
* ```mv <target> <newtargetname>``` Used to move or rename a file.
* ```rm <filename>``` Remove file
* ```cp <filename>``` Copies filename

### Directory Management
* ```mkdir <dirname>``` Make Directory 
* ```rmdir <directoryname>``` Remove directory

### Package Management
* ```sudo apt update``` Update - retrieve latest files for programs
* ```sudo apt upgrade``` Upgrade - unpack latest files for programs
* ```sudo apt install <packagename>``` Download as superuser

