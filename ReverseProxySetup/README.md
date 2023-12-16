# Setting up a Reverse Proxy


## What is a Reverse Proxy?
A reverse proxy handles requests on behalf of a server. When a client makes a request to a particular resource, the reverse proxy intercepts that request and forwards it to the appropriate server. The server's response then goes back through the reverse proxy before reaching the client. They can be used for a number of different functions including:
* Load Balancing - redirecting to different servers based on workload
* Port Mapping - mapping port requests to the appropriate port
* URL Rewriting - changing paths, adding parameters or redirecting to other resources

## Goals:
We would like it so that whenever a user enters our VM's public IP address, they will be automatically be redirected to port 5000 so that they can access the website. This is known as Port Mapping.

## Prerequisites
We are using the previous BASH file created to run our spring boot server - this helps us deal with the deployment of our app. Whenever a user enters our VM's IP address without a port, the default port 80 will be used.

## Installing Apache2
Apache2 must first be installed, as well as enabling its modules followed by a restart. This can be achieved by the following sequential commands. By enabling the relevant apache proxy modules, this allows Apache2 to peform proxying, notably in HTTP and HTTPS.

```
# Install Apache2
sudo DEBIAN_FRONTEND=noninteractive apt install apache2 -y

# Enable relevant apache proxy modules
sudo a2enmod proxy -y
sudo a2enmod proxy_http -y

# Restart Apache 
sudo systemctl restart apache2 
```

## How Apache2 works
For this tutorial specifically, we will focus on the ```sites-enabled``` and the ```sites-active``` folder.

**sites-available:** This directory holds configuration files for different websites or applications that could potentially be used by Apache. It's like a storage area for various configurations.

**sites-enabled:** This directory contains the active configurations that Apache is currently using. It's like a list of "enabled" websites or applications that Apache is actively serving.

When you want Apache to use a configuration file from `sites-available`, you move (or link) it into `sites-enabled`. When you want to stop using a configuration file, you remove it from `sites-enabled`.

In essence, `sites-available` is a collection of options, and `sites-enabled` is the list of options currently in use by Apache.

## Inside the sites-enabled directory
By default, inside the folder exists a config file named ```000-default.config```. The code inside should look like:
```
<VirtualHost *:80>
    DocumentRoot /var/www/example.com
    # Other stuff
</VirtualHost>
```
We can add a redirect initiative to redirect the user not only to a specific URL, but also a specific port number. Here we will assume 2.12.25.102 is our public IP address.

```
<VirtualHost *:80>
    DocumentRoot /var/www/example.com
    # Other stuff
    Redirect / http://2.12.25.102:5000/
</VirtualHost>
```

Now we have manually configured a file to redirect to port 5000 for our server. The problem is that the IP can be dynamic and some finesse will be required to handle this change in dynamic IPs.

## A Bash Script for Changing the Config

We will need an external shell to change our config file. As we know the Redirect line is the target line to be changed, we will simply need to grab our IP using the curl command, calculate the full redirect URL and perform a change.

Here we will use the sed command to search for a specific line that contains the Redirect pattern, and replace it with our new URL. The sed command will usually take 3 parameters, the pattern to find, the pattern to replace with and the target file.

```
# Fetch the public IP using curl
PUBLIC_IP=$(curl ifconfig.me)

# Create the new Redirect Line
REPLACEMENT_LINE="Redirect / http://$PUBLIC_IP:5000/"

# Replace IP in config file
sudo sed -i "/Redirect/ s|.*|$REPLACEMENT_LINE|" /etc/apache2/sites-enabled/000-default.conf

# Restart Apache
sudo systemctl reload apache2
```


## Our New Bash File
In addition to our old bash file, we have:
```
#!/bin/bash

# Update
echo "Updating"
sudo apt update -y
echo ""

# Upgrade
echo "Upgrading"
sudo DEBIAN_FRONTEND=noninteractive apt upgrade -y
echo ""

# Install maven
echo "Installing Maven"
sudo DEBIAN_FRONTEND=noninteractive apt install maven -y
echo ""

# Check maven install
echo "Checking Maven Install:"
mvn -version
echo ""

# Install JDK Java 17
echo "Installing JDK 17"
sudo DEBIAN_FRONTEND=noninteractive apt install openjdk-17-jdk -y
echo ""

# Check java version
echo "Checking Java Install:"
java -version
echo ""

# Clone App from Git
git clone https://github.com/Affiq/tech242-jsonvorhees-app.git

# CD into springapi folder
cd tech242-jsonvorhees-app/jsonvoorhees-java-atlas-app/springapi/

# Springboot start...
mvn spring-boot:start

# OUR NEW CODE
# Install Apache2
sudo DEBIAN_FRONTEND=noninteractive apt install apache2 -y

# Enable relevant apache proxy modules
sudo a2enmod proxy -y
sudo a2enmod proxy_http -y

# Restart Apache 
sudo systemctl restart apache2 

# Fetch the public IP using curl
PUBLIC_IP=$(curl ifconfig.me)

# Set the environment variable
export MY_PUBLIC_IP=$PUBLIC_IP

# Create the new Redirect Line
REPLACEMENT_LINE="Redirect / http://$PUBLIC_IP:5000/"

# Replace IP in config file
sudo sed -i "/Redirect/ s|.*|$REPLACEMENT_LINE|" /etc/apache2/sites-enabled/000-default.conf

# Restart Apache
sudo systemctl reload apache2


```
