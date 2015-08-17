# Linux-Server-Configuration-UDACITY
This is the fifth project for "Full Stack Web Developer Nanodegree" on Udacity. 

In this project, a Linux virtual machine needs to be configurated to support the Item Catalog website.

## Tasks
1. Launch your Virtual Machine with your Udacity account
2. Follow the instructions provided to SSH into your server
3. Create a new user named grader
4. Give the grader the permission to sudo
5. Update all currently installed packages
6. Change the SSH port from 22 to 2200
7. Configure the Uncomplicated Firewall (UFW) to only allow incoming connections for SSH (port 2200), HTTP (port 80), and NTP (port 123)
8. Configure the local timezone to UTC
9. Install and configure Apache to serve a Python mod_wsgi application
10. Install and configure PostgreSQL:
	- Do not allow remote connections
	- Create a new user named catalog that has limited permissions to your catalog application database
11. Install git, clone and setup your Catalog App project (from your GitHub repository from earlier in the Nanodegree program) so that it functions correctly when visiting your server’s IP address in a browser. Remember to set this up appropriately so that your .git directory is not publicly accessible via a browser!

## Launch Virtual Machine
### Instructions for SSH access to the instance
1. Download Private Key below
2. Move the private key file into the folder `~/.ssh` (where ~ is your environment's home directory). So if you downloaded the file to the Downloads folder, just execute the following command in your terminal.
	```mv ~/Downloads/udacity_key.rsa ~/.ssh/```
3. Open your terminal and type in
	```chmod 600 ~/.ssh/udacity_key.rsa```
4. In your terminal, type in
	```ssh -i ~/.ssh/udacity_key.rsa root@52.24.125.52```
5. Development Environment Information

	Public IP Address

	52.24.125.52
	
	Private Key ( is not provided here. )

## Create a new user named grader
1. `sudo adduser grader`
2. `vim /etc/sudoers`
3. `touch /etc/sudoers.d/grader`
4. `vim /etc/sudoers.d/grader`, type in `grader ALL=(ALL:ALL) ALL`, save and quit

## Set ssh login using keys
1. generate keys on local machine using`ssh-keygen` ; then save the private key in `~/.ssh` on local machine
2. deploy public key on developement enviroment

	On you virtual machine:
	```
	$ su - grader
	$ mkdir .ssh
	$ touch .ssh/authorized_keys
	$ vim .ssh/authorized_keys
	# Copy the public key generated on your local machine to this file and save
	$ chmod 700 .ssh
	$ chmod 644 .ssh/authorized_keys
	```
	
3. reload SSH using `service ssh restart`
4. now you can use ssh to login with the new user you created

	`ssh -i \[privateKey\] grader@52.24.125.52`

## Update all currently installed packages

	```
	$ sudo apt-get update
	$ sudo apt-get upgrade
	```

## Change the SSH port from 22 to 2200

	```
	$ sudo vim /etc/ssh/sshd_config
	# change Port 22 to Port 2200 , save & quit
	# reload SSH
	$ sudo service ssh restart
	```
## Configure the Uncomplicated Firewall (UFW)

	```
	# Configure the Uncomplicated Firewall (UFW) to only allow incoming connections for SSH (port 2200), HTTP (port 80), and NTP (port 123)
	$ sudo ufw allow 2200/tcp
	$ sudo ufw allow 80/tcp
	$ sudo ufw allow 123/udp
	$ sudo ufw enable 
	```
## Configure the local timezone to UTC

	```
	```

## Install and configure Apache to serve a Python mod_wsgi application


	```
	# Install Apache
	$ sudo apt-get install apache2
	#Install mod_wsgi
	$ apt-get install python-setuptools libapache2-mod-wsgi
	# Restart Apache
	$ sudo service apache2 restart
	```

Install Apache sudo apt-get install apache2
Install mod_wsgi sudo apt-get install python-setuptools libapache2-mod-wsgi
Restart Apache sudo service apache2 restart

