# Storing .pem in .ssh
- [Storing .pem in .ssh](#storing-pem-in-ssh)
  - [Setting up the Private Key](#setting-up-the-private-key)
  - [Changing Permissions](#changing-permissions)

## Setting up the Private Key
A .ssh folder should exist in your root folder so C://Users/username/. You should then navigate to the .ssh folder in which you should move your .pem file (private key). Ensure that the private key does not persist in the download folder.

## Changing Permissions
To ensure the existence of the private key, use ```ls -l``` that the private key is not publicly viewable. This command allows you to also view the permissions of the key (read,write, execute). The command: ```chmod 400 privatekeyname.pem``` can also be used set the permissions to read only by the user.

