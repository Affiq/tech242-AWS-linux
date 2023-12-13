# More on Linux
- [More on Linux](#more-on-linux)
  - [Package Management](#package-management)
  - [BASH Scripting](#bash-scripting)
    - [Creating a new BASH Script](#creating-a-new-bash-script)
    - [Development Process](#development-process)
    - [Response](#response)
  - [Processes](#processes)
    - [Theory](#theory)
    - [Components](#components)
  - [Process Commands](#process-commands)


## Package Management
* Package files can be retrieved using ```sudo apt update -y```
* Package files can be updated (which could cause potential errors) using ```sudo apt upgrade -y```
  
## BASH Scripting
### Creating a new BASH Script
* A new file can be created using ```nano <scriptname>```
  * ```touch <scriptname>``` can also be used, but nano deals with file creation.
* Using the nano editor, add the shebang followed by the BASH identifier to allow the file to understand that it is a BASH script. In our example, we would like to create a shell that will always automatically start the latest Nginx application.
```
#!/bin/bash
```
### Development Process
* Typically when approaching BASH scripts, planning is required and so pseudocommands should be written down first to outline the main steps towards an end goal.
* It is also wise to typically test each command individually to catch potential hangs or errors further down the line, such as adding a -y flag for some commands or a sudo prefix to enable access to some commands. In our given instance, we produce the following skeleton shell.
```
#!/bin/bash

# update latest packages

# upgrade lastest packages

# install nginx webserver

# restart nginx

# enable nginx

```
### Response
* Once we have tested and defined our shell program is fully functional, we can also observe that our program is not very feedback friendly. The use of well placed echo commands can notify the end user of some input. Making space of blank line echos can also help chunk particular command responses. This helps us produce our final shell which looks like this.

```
#!/bin/bash

# update latest packages
echo "Updating..."
sudo apt update -y
echo "Updating: Done"
echo ""

# upgrade lastest packages
echo "Upgrading..."
sudo apt upgrade -y
echo "Upgrading: Done"
echo ""

# install nginx webserver
echo "Installing..."
sudo apt install nginx -y
echo "Installing: Done"
echo ""

# restart nginx
echo "Restarting..."
sudo systemctl restart nginx
echo "Restarting: Done"
echo ""

# enable nginx
echo "Enabling..."
sudo systemctl enable nginx
echo "Enabling: Done"
echo ""

```

This allows us to achieve a BASH script which is both functional and terminal responsive.
Screenshot

## Processes
### Theory
* A process is something in memory, and can possibly be using the CPU.
* Single-core Machines don't actually run processes concurrently - they switch and allocate a portion of the CPU to the respective processes.
* Processes must wait in a queue before being able to be executed.
* Two types of processes exist:
  * System Processes - Do not provide applications/interfaces for end users, usually provide services such as Drivers, Files, Logging, etc.
  * User Processes - Include applications and tasks initiated by users on the system.
* The init process with PID 1 is usually responsible for spawning all the relevant processes needed within the operating system
  
### Components
* PID: Every time a processes starts, it is allocated a unique Process ID. 
* TTY: Tele-TypeWriter - linked terminal/interface. User Processes are typically linked to a terminal (TTY) while System Processes are not.
* CMD: Relevant command linked with the process.
  

## Process Commands
* ```ps aux``` Extremely detailed