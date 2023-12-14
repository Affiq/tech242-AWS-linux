# Storing .pem in .ssh
- [Storing .pem in .ssh](#storing-pem-in-ssh)
  - [Setting up the Private Key](#setting-up-the-private-key)
  - [Creating a Folder](#creating-a-folder)
  - [Confirming the .ssh Folder](#confirming-the-ssh-folder)
  - [Changing Permissions](#changing-permissions)

## Setting up the Private Key
A .ssh folder should exist in your root folder so C://Users/username. You should then navigate to the .ssh folder in which you should move your .pem file (private key). Ensure that the private key does not persist in the download folder.

## Creating a Folder

## Confirming the .ssh Folder
To confirm the existence of the .ssh folder in the right location, use the following command ```cd ~/.ssh -a``` as the tilde is symbolic of the Window's user's root directory. When using ```ls``` to view the folder, remember to add the ```-a``` flag to view hidden folders.

## Changing Permissions
To ensure the existence of the private key, use ```ls -l``` inside the .ssh folder to ensure that the private key is not publicly viewable. This command allows you to also view the permissions of the key (read,write, execute). The command: ```chmod 400 privatekeyname.pem``` can also be used set the permissions to read only by the user.

