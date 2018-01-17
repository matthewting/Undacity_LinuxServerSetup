# Undacity_LinuxServerSetup

## IP Address: 54.213.242.166
## URL: http://ec2-54-213-242-166.us-west-2.compute.amazonaws.com
## port for SSH: 2200
## grader password: P@ssw0rd!123
## Summary of software installed:

	1. Flask
	2. PostgreSQL
	3. Sqlalchemy
	4. Oatu2Client
	5. psycopg2
## Summary of configurations made:
	1. Set up grader
		- $ sudo adduser grader
		- Add "grader ALL=(ALL:ALL) ALL" text into the /etc/sudoers.d/grader
		- Set grader password using:
			$ passwd grader
		- I set it as "P@ssw0rd!123"
		
	2. Create key pair for grader and added into grader's authorized key
		- (local machine)$ssh-keygen
		- set the private key file to grader.rsa and copy to ~/.ssh/
		- set the public key file to grader.pub and also copy to ~/.ssh/
		- $sudo mkdir /home/grader/.ssh
		- $sudo nano /home/grader/.ssh/authorized_keys
		- put the content of the grader.pub into this authorized_keys file and save
		- restart the ssh to make change effective: $sudo service ssh restart
		- Now the grader can login with the rsa file like:
			$ ssh -i ~/.ssh/grader.rsa grader@54.213.242.166

	3. Disabled root login
		- Clear up everything from the root ssh keys:
			$ sudo nano /home/root/.ssh/authorized_keys
			
	4. Change the ssh port to 2200
		- Enable the port 2200 from lightsail firewall portal
		- Edit the sshd_config by: 
			$ sudo nano /etc/ssh/sshd_config
			- change Port 22 to Port 2200
			- change PermitRootLogin to PermitRootLogin no
			- change PasswordAuthentication to PasswordAuthentication no
		- restart the ssh to make change effective: $sudo service ssh restart
		- Now the grader can login with the rsa file like:
			$ ssh -i ~/.ssh/grader.rsa grader@54.213.242.166 -p 2200
		
	5. Enabled firewall and only allow 80, 2200 and 123 port connections
		- login ssh and configure the firewall and ports
			$ sudo ufw default deny incoming
			$ sudo ufw default allow outgoing
			$ sudo ufw allow 2200
			$ sudo ufw allow 2200/tcp
			$ sudo ufw allow 80
			$ sudo ufw allow 80/tcp
			$ sudo ufw allow 123
			$ sudo ufw allow 123/tcp
		- After configured, activate the firewall and check the status to confirm
			$ sudo ufw enable
			$ sudo ufw status

	6. Updated all the package
		- $ sudo apt-get update
		- $ sudo apt-get upgrade
		
	7. Install Apache, WSGI, and Git, followed by installing my catalog project
		- install the apache 2: $ sudo apt-get install apache2
		- install WSGI for Apache:
			$ sudo apt-get install python-setuptools
			$ sudo apt-get install libapache2-mod-wsgi
		- Enable WSGI: 
			$ sudo a2enmod wsgi
		- Restart apache:
			$ sudo service apache2 restart
		- we can check to see if the default Apache page is loaded or not by visiting the IP address:
			http://54.213.242.166
			
		- install the Git: $sudo apt-get install git-all 
			
	8. Create and set up the PostgreSQL database
	9. Configure the catalog project to make it able to be enabled in public using flask
		- renamed the original view.py to __init__.py
		- updated all the engine from  
			engine = create_engine('sqlite:///catalog.db')  
		  to
		  	engine = create_engine("postgresql://catalog:catalog@localhost/catalog")
			
		- Change the application run statement from 
			app.run(host='0.0.0.0', port=8000)
		  to
		  	app.run()

	10. Configure the PSQL  database to support the catalog project
	11. Added the new public domain url to my google key 
## List of third party resources used to complete this project:
	1. SSH
	2. Terminal
	3. AWS Lightsail web portal
	4. Udacity Forum
