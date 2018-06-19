# Linux server configuration project

## About Project

Take a Linux distribution on a virtual machine and prepare it to host your web applications, to include installing updates, securing it from attacks and installing web and database servers.

IP address: 35.167.27.204

Accessible SSH port: 2200

Application URL: 

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


