# SSH - Pushing to GitHub

We will first need to navigate to our .ssh folder to generate our key-pair. We will use the following command:
```ssh-keygen -t rsa -b 4096 -C "email"```
* Where ```-t rsa``` specifies to use the RSA algorithm
* ```-b 4096``` specifies the bytes to use for the keys
* ```-C "email"``` specifies the owner of the key.

It will then prompt you for the name of a key file, and a passphrase for the key (which you can optionally leave blank).