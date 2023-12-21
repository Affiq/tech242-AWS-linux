# Quickstart BASH Scripts

- [Quickstart BASH Scripts](#quickstart-bash-scripts)
  - [Note](#note)
  - [Nginx Server Setup](#nginx-server-setup)
  - [Spring-Boot Server Setup](#spring-boot-server-setup)
  - [Apache2 Reverse Proxy Setup](#apache2-reverse-proxy-setup)
  - [SQL Server Setup](#sql-server-setup)


## Note
It is important to test each step manually unless you are following the exact same tutorial and are not worried about understanding. These scripts are placed here as some components may provide overlap which some people may find useful and adjust for their project.

## Nginx Server Setup
The following script simply sets up a Nginx server.

```
#!/bin/bash
GREEN='\e[32m'
NO_COLOR='\e[0m'

# update latest packages
echo "Updating..."
sudo apt update -y
echo -e "Updating: ${GREEN}Done${NO_COLOR}"
echo ""

# upgrade lastest packages
echo "Upgrading..."
sudo apt upgrade -y
echo -e "Upgrading: ${GREEN}Done${NO_COLOR}"
echo ""

# install nginx webserver
echo "Installing..."
sudo apt install nginx -y
echo -e "Installing: ${GREEN}Done${NO_COLOR}"
echo ""

# restart nginx
echo "Restarting..."
sudo systemctl restart nginx
echo -e "Restarting: ${GREEN}Done${NO_COLOR}"
echo ""

# enable nginx
echo "Enabling..."
sudo systemctl enable nginx
echo -e "Enabling: ${GREEN}Done${NO_COLOR}"
echo ""
```

## Spring-Boot Server Setup
The following script deals with the setup of a Spring Boot server. Adjust JDK used in the install and any other software dependencies. Also configure the corresponding clone and change directory methods to your relevant setup.

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

# Install JDK Java 17 - CHANGE ACCORDINGLY
echo "Installing JDK 17"
sudo DEBIAN_FRONTEND=noninteractive apt install openjdk-17-jdk -y
echo ""

# Check java version
echo "Checking Java Install:"
java -version
echo ""

# Clone App from Git - CHANGE ACCORDINGLY
git clone https://github.com/Affiq/tech242-jsonvorhees-app.git

# CD into springapi folder - CHANGE ACCORDINGLY
cd tech242-jsonvorhees-app/jsonvoorhees-java-atlas-app/springapi/

# Springboot start...
mvn spring-boot:start

```

## Apache2 Reverse Proxy Setup
The following scripts deals with installing Apache2 and enabling the relevant modules, as well as configuring a port mapping. To change the port number, simply replace all instances of ```localhost:5000``` with ```localhost:<port-number>```.

```
# Install Apache2
sudo DEBIAN_FRONTEND=noninteractive apt install apache2 -y

# Enable relevant apache proxy modules
sudo a2enmod proxy
sudo a2enmod proxy_http

# Restart Apache 
sudo systemctl restart apache2 

# Edit config file if not configured - CHANGE ACCORDINGLY
if grep -q 'ProxyPass / http://localhost:5000/' /etc/apache2/sites-available/000-default.conf; then
    # The string exists, so nothing to do
    echo "Reverse proxy already configured."
else
    # reverse proxy not configured yet
    echo "Reverse proxy NOT configured."
    # CHANGE ACCORDINGLY
    sudo sed -i '/DocumentRoot \/var\/www\/html/ a\ProxyPreserveHost On\nProxyPass \/ http:\/\/localhost:5000\/\nProxyPassReverse \/ http:\/\/localhost:5000\/\n' /etc/apache2/sites-available/000-default.conf
fi

# Restart Apache
sudo systemctl reload apache2
```

## SQL Server Setup
The following code covers the installation of a MySQL server, the creation of a database, running a SQL file to extract the data and also the creation of a MySQL user so that other VMs may connect and access the database.

```
#!/bin/bash

# Update
echo "Updating"
sudo apt update -y
echo "Updating: Done"
echo ""

# Upgrade
echo "Upgrading"
sudo DEBIAN_FRONTEND=noninteractive apt upgrade -y
echo "Upgrading: Done"
echo ""

# Install MySQL
echo "Installing MySQL Server"
sudo DEBIAN_FRONTEND=noninteractive apt install mysql-server -y
echo "Installation: Done"
echo ""

# Start MYSQL on boot
echo "Enabling MySQL"
sudo systemctl enable mysql
echo "Enabling: Done"
echo ""

# Enable remote connections
echo "Opening connections"
# CHANGE ACCORDINGLY TO CORRECT APPLICATION LAYER VM ADDRESS
sudo sed -i 's/^bind-address\s*=\s*127\.0\.0\.1/bind-address = 0.0\.0\.0/' /etc/mysql/mysql.conf.d/mysqld.cnf
echo "Connection setup: Done"
echo ""

# Restart MySQL
echo "Restarting MySQL"
sudo systemctl restart mysql.service
echo "Restarting: Done"
echo ""

# Cloning database file - CHANGE ACCORDINGLY TO REPO
echo "Cloning database repo"
sudo git clone https://github.com/Affiq/World_SQL_Database.git repo
echo "Cloning: Done"
echo ""

# Create new user for VM to connect to - CHANGE ACCORDINGLY TO DESIRED SQL USER DETAILS
echo "Creating new MySQL User"
sudo mysql -e "CREATE USER 'root'@'%' IDENTIFIED BY 'root'; GRANT ALL PRIVILEGES ON *.* TO 'root'@'%'; FLUSH PRIVILEGES;"
echo "User Creation: Done"
echo ""

# Create new database - CHANGE ACCORDINGLY TO DESIRED DATABASE NAME
echo "Creating database"
sudo mysql -u root -p'root' -h localhost -P 3306 -e "CREATE DATABASE world;"
echo "Database creation done"
echo ""

# Extract SQL data - CHANGE ACCORDINGLY TO RIGHT DIRECTORY, DATABASE NAME AND SQL FILE
echo "Extracting MySQL file"
cd /repo
sudo mysql -u root -p'root' -h localhost -P 3306 -D world < world.sql
echo "Extraction: Done"
echo ""

# Show Databases
echo "Showing Databases..."
sudo mysql -e "SHOW DATABASES;"
echo ""
```