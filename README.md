# Linux server configuration project

## About Project

Take a Linux distribution on a virtual machine and prepare it to host your web applications, to include installing updates, securing it from attacks and installing web and database servers.

The list of software installed are:

1. Python

2.Postgresql

3.Flask environment

4. Apache2

IP address: 35.167.27.204

Accessible SSH port: 2200
 

## Set-up Process

1.Create a new user with name grader and give it permissions to sudo.

* Use the command ssh -i ~/.ssh/udacity_key.rsa root@35.167.27.204 to get SSH into the server.

* To create a new user named grader run the command $ sudo adduser grader.

* Run the command sudo nano /etc/sudoers.d/grader to create a new file in directory.

* Add the following text grader ALL=(ALL:ALL) ALL.

* Run sudo nano /etc/hosts.

* Update the installed packages and download package lists using the command sudo apt-get update.

* Get new versions of packages using the command sudo apt-get upgrade.

## Changing the port

* Change SSH port from 22 to 2200.

* Run sudo nano /etc/ssh/sshd_config.

* Change the port from 22 to 2200.

## Configure the Firewall to only allow incoming connections for SSH , HTTP and NTP

* sudo ufw allow 2200/tcp
* sudo ufw allow 80/tcp
* sudo ufw allow 123/udp
* sudo ufw enable

## Create a new user named grader

sudo adduser grader

vim /etc/sudoers

touch /etc/sudoers.d/grader

vim /etc/sudoers.d/grader, type in grader ALL=(ALL:ALL) ALL, save and quit

Set ssh login using keys

generate keys on local machine usingssh-keygen ; then save the private key in ~/.ssh on local machine

deploy public key on developement enviroment

On you virtual machine:

$ su - grader

$ mkdir .ssh

$ touch .ssh/authorized_keys

$ vim .ssh/authorized_keys

Copy the public key generated on your local machine to this file and save

$ chmod 700 .ssh

$ chmod 644 .ssh/authorized_keys

reload SSH using service ssh restart

now you can use ssh to login with the new user you created

ssh -i [privateKeyFilename] grader@52.24.125.52

## Update all currently installed packages

sudo apt-get update

sudo apt-get upgrade

Change the SSH port from 22 to 2200

Use sudo vim /etc/ssh/sshd_config and then change Port 22 to Port 2200 , save & quit.

Reload SSH using sudo service ssh restart

Configure the Uncomplicated Firewall (UFW)

Configure the Uncomplicated Firewall (UFW) to only allow incoming connections for SSH (port 2200), HTTP (port 80), and NTP (port 123)

sudo ufw allow 2200/tcp

sudo ufw allow 80/tcp

sudo ufw allow 123/udp

sudo ufw enable 

## Configure the local timezone to UTC

Configure the time zone sudo dpkg-reconfigure tzdata

It is already set to UTC.

Install and configure Apache to serve a Python mod_wsgi application

Install Apache sudo apt-get install apache2

Install mod_wsgi sudo apt-get install python-setuptools libapache2-mod-wsgi

Restart Apache sudo service apache2 restart

Install and configure PostgreSQL

Install PostgreSQL sudo apt-get install postgresql

Check if no remote connections are allowed sudo vim /etc/postgresql/9.3/main/pg_hba.conf

Login as user "postgres" sudo su - postgres

Get into postgreSQL shell psql

## Create a new database named catalog and create a new user named catalog in postgreSQL shell

postgres=# CREATE DATABASE catalog;

postgres=# CREATE USER catalog;

Set a password for user catalog

postgres=# ALTER ROLE catalog WITH PASSWORD 'password';

Give user "catalog" permission to "catalog" application database

postgres=# GRANT ALL PRIVILEGES ON DATABASE catalog TO catalog;

Quit postgreSQL postgres=# \q

## Exit from user "postgres"

exit

Install git, clone and setup your Catalog App project.

Install Git using sudo apt-get install git

Use cd /var/www to move to the /var/www directory

Create the application directory sudo mkdir FlaskApp

Move inside this directory using cd FlaskApp

Clone the Catalog App to the virtual machine git clone https://github.com/kongling893/Item_Catalog_UDACITY.git

Rename the project's name sudo mv ./Item_Catalog_UDACITY ./FlaskApp

Move to the inner FlaskApp directory using cd FlaskApp

Rename website.py to __init__.py using sudo mv website.py __init__.py

Edit database_setup.py, website.py and functions_helper.py and change engine = create_engine('sqlite:///toyshop.db') to engine = create_engine('postgresql://catalog:password@localhost/catalog')

## Install pip sudo apt-get install python-pip

Use pip to install dependencies sudo pip install -r requirements.txt

Install psycopg2 sudo apt-get -qqy install postgresql python-psycopg2

Create database schema sudo python database_setup.py

Configure and Enable a New Virtual Host

Create FlaskApp.conf to edit: sudo nano /etc/apache2/sites-available/FlaskApp.conf

Add the following lines of code to the file to configure the virtual host.

<VirtualHost *:80>

	ServerName 52.24.125.52
  
	ServerAdmin qiaowei8993@gmail.com
  
	WSGIScriptAlias / /var/www/FlaskApp/flaskapp.wsgi
  
	<Directory /var/www/FlaskApp/FlaskApp/>
  
		Order allow,deny
    
		Allow from all
    
	</Directory>
  
	Alias /static /var/www/FlaskApp/FlaskApp/static
  
	<Directory /var/www/FlaskApp/FlaskApp/static/>
  
		Order allow,deny
    
		Allow from all
    
	</Directory>
  
	ErrorLog ${APACHE_LOG_DIR}/error.log
  
	LogLevel warn
  
	CustomLog ${APACHE_LOG_DIR}/access.log combined
  
</VirtualHost>

Enable the virtual host with the following command: sudo a2ensite FlaskApp

Create the .wsgi File

Create the .wsgi File under /var/www/FlaskApp:

cd /var/www/FlaskApp

sudo nano flaskapp.wsgi 

Add the following lines of code to the flaskapp.wsgi file:

#!/usr/bin/python

import sys

import logging

logging.basicConfig(stream=sys.stderr)

sys.path.insert(0,"/var/www/FlaskApp/")


from FlaskApp import app as application

application.secret_key = 'Add your secret key'

## Install Apache 2

https://httpd.apache.org/download.cgi

https://apache-http-server.en.softonic.com

## Restart Apache

Restart Apache sudo service apache2 restart



