Research Managing File Ownership
Research Managing File Permissions
Research Managing File Permissions Using Numbers
Research if normal user can kill processes owned by root
Redirection and Appending in Linux


- [File Ownership Importance](#file-ownership-importance)
  - [Basics](#basics)
  - [Changing Permissions](#changing-permissions)
  - [Changing Permissions with Numbers](#changing-permissions-with-numbers)
- [Group Management](#group-management)
  - [Viewing Groups](#viewing-groups)
  - [Adding, Deleting and Modifying Groups](#adding-deleting-and-modifying-groups)
  - [Changing Ownership Groups](#changing-ownership-groups)


# File Ownership Importance
## Basics

File ownership is important for a number of various reasons:
* Access Control - determines who has RWX permissions
* Security - helps enforce security - root files typically have locked off access
* Ease of Group Collaboration - group permissions allow easy assignment of permissions to many people
* System Administration - Compartmentalised control allows authorisation to essential components of the system

```ls -l``` command can be used to view ownership, typically being the first string.

When a user creates a file, the ownership and group ownership is typically assigned to the logged.
Execution is not given automatically when creating a file as to prevent the execution of any arbitrary code within the operating system.

## Changing Permissions


## Changing Permissions with Numbers
Each permission is allocated a specific number:

| Permission | Description |
|------------|-------------|
| 4          | Read        |
| 2          | Write       |
| 1          | Execute     |

A combination of these numbers (as per how binary functions) 


# Group Management

In Linux systems, groups are used to organise and manage collections of users and their access to some file or directories.
* Being the owner of a file or directory does not necesarily mean you have RWX permissions - for instance, service files in root can be made which are not meant to be RWXed by the user!
* Permissions by the user entity can be performed if the user is logged in accordingly
* Permissions by the group entity can be performed if the user that is logged in belongs to that group
* Permissions by the other entity can be performed by anyone.
  
For example, given the terminal output:
```-rwxr-xr-- 1 tcboony staff  123 Nov 25 18:36 keeprunning.sh```
We can deduce that (with respect to keeprunning.sh): 
| Entity     | Permission  |
|------------|-------------|
| tcboon     | RWX         |
| staff      | R-X         |
| other      | R--         |

Which can be interpreted as:
* User 'tcboony' has read, write, execute permissions
* The group 'staff' has read and execute permissions
* Other users only have read access.

The following functionality can be achieved using:
```chmod 754 keeprunning.sh```

The following command ```chmod 644``` will produce -rw--r--r-- permissions, so readable by everyone and writable by user only.

## Viewing Groups
* The ```getent group``` command will get all entries within the group file.
* Alternatively, you can use ```cat /etc/group``` to obtain the entries.
* The typical format is listed as ```<groupname>:<groupID>:<users in group>```
* This excludes root who is the superuser and has unrestricted access to the entire system, thus this does not need to be listed in particular groups.
* When a user is created, they will be assigned and have control over their own primary group. Typcally when we log into a VM, this will be shown as ```ubuntu:<id>:ubuntu```
* Users can then be assigned a secondary group to allow users to have more privileges within their system.

Screenshot

## Adding, Deleting and Modifying Groups
* A new group can be created using the ```sudo groupadd <groupname>``` command
* An existing group can be deleted using the ```sudo groupdel <groupname>``` command
* Users can be added using the ```sudo usermod -aG <groupname> <username>``` command

## Changing Ownership Groups
* ```sudo chown :<groupname> <directoryname>``` can be used to transfer ownership to a group
* ```sudo chown <username>: <directoryname>``` can be used to transfer ownership to a user

