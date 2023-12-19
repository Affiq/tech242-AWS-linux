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

## Redirecting with sites-enabled directory
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

## Using Proxy Pass with sites-active directory
We can also use a number of proxy pass settings within the ```sites-active``` directory to perform port mapping. This can be done by adding the following 3 settings into the file.

```

```


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


## Naive BASH Script
By combining the earlier Spring-Boot deployment setup along with the apache2 setup, we have a functioning BASH script to deploy both the Java applet and the reverse proxy.

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
sudo a2enmod proxy
sudo a2enmod proxy_http

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


## Configuration File Modification Using SED
We would like to create a code block that will modify the code block given that the settings are not yet configured. The first step is to first create our code that will inject the desired seetings into our 000-default.conf file.

```
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html
    # Injected settings
    ProxyPreserveHost On
    ProxyPass / http://localhost:5000/
    ProxyPassReverse / http://localhost:5000/
```

We can then do this by formatting the following settings into one line, and use the SED command to look for the DocumentRoot line. The a\ flag before ProxyPreserveHost allows us to add the following lines rather than replace them.

```
    sudo sed -i '/DocumentRoot \/var\/www\/html/ a\ProxyPreserveHost On\nProxyPass \/ http:\/\/localhost:5000\/\nProxyPassReverse \/ http:\/\/localhost:5000\/\n' /etc/apache2/sites-available/000-default.conf
```

### Determining Configured or Not
With the following settings in mind, it is trivial to determine whether our proxy is configured, if the following settings are not in the file then it has not yet been configured. Therefore, we can use grep to determine if the pattern exists in the file. Here we will choose an arbritrary line unique to these settings. It is important not to use ProxyPreserveHost as this is NOT unique to our specific configuration, and alternate configurations may interfere with this.

```grep -q 'ProxyPass / http://localhost:5000/' /etc/apache2/sites-available/000-default.conf```

We can further combine this into an if statement with an echo command to then determine if the proxy is configured using the following command:

```
if grep -q 'ProxyPass / http://localhost:5000/' /etc/apache2/sites-available/000-default.conf; then
    # The string exists, so nothing to do
    echo "Reverse proxy already configured."
else
    # reverse proxy not configured yet
    echo "Reverse proxy NOT configured."
fi
```

### Configuration Code Block
Once we have manually tested the steps and are comfortable about our Configuration detection code block, we can then move the actual sed command into the code block to create our Configuration editor block. It is important to test this code block for the following cases:
* When no configuration exists
* When the configuration exists
* When multiple configuration exists


```
if grep -q 'ProxyPass / http://localhost:5000/' /etc/apache2/sites-available/000-default.conf; then
    # The string exists, so nothing to do
    echo "Reverse proxy already configured."
else
    # reverse proxy not configured yet
    echo "Reverse proxy NOT configured."
    sudo sed -i '/DocumentRoot \/var\/www\/html/ a\ProxyPreserveHost On\nProxyPass \/ http:\/\/localhost:5000\/\nProxyPassReverse \/ http:\/\/localhost:5000\/\n' /etc/apache2/sites-available/000-default.conf
fi
```

### End Result
From here we create a BASH scripts that is functional as a singular BASH script. After running this in a fresh VM, we can then test this in the User Data of a fresh virtual machine before attempting to move this into an AMI.

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
# Nav back to root
cd /

# Install Apache2
sudo DEBIAN_FRONTEND=noninteractive apt install apache2 -y

# Enable relevant apache proxy modules
sudo a2enmod proxy
sudo a2enmod proxy_http

# Restart Apache 
sudo systemctl restart apache2 

# Edit config file if not configured
if grep -q 'ProxyPass / http://localhost:5000/' /etc/apache2/sites-available/000-default.conf; then
    # The string exists, so nothing to do
    echo "Reverse proxy already configured."
else
    # reverse proxy not configured yet
    echo "Reverse proxy NOT configured."
    sudo sed -i '/DocumentRoot \/var\/www\/html/ a\ProxyPreserveHost On\nProxyPass \/ http:\/\/localhost:5000\/\nProxyPassReverse \/ http:\/\/localhost:5000\/\n' /etc/apache2/sites-available/000-default.conf
fi

# Restart Apache
sudo systemctl reload apache2

```
