# Undacity_LinuxServerSetup

# IP Address: 54.213.242.166
# URL: http://ec2-54-213-242-166.us-west-2.compute.amazonaws.com
# port for SSH: 2200
# Summary of software installed:
	1. Flask
	2. PostgreSQL
	3. Sqlalchemy
	4. Oatu2Client
	5. psycopg2
# Summary of configurations made:
	1. Set up grader
		
	2. Create key pair for grader and added into grader's authorized key
	3. Disabled root login
	4. Change the ssh port to 2200
	5. Enabled firewall and only allow 80, 2200 and 123 port connections
	6. Updated all the package
	7. Git install my catalog project
	8. Create and set up the PostgreSQL database
	9. Configure the catalog project to make it able to be enabled in public using flask
		- renamed the original view.py to __init__.py
		- updated all the engine from  
```
			engine = create_engine('sqlite:///catalog.db')  
```
		  to
```
		  	engine = create_engine("postgresql://catalog:catalog@localhost/catalog")
```
			
		- Change the application run statement from 
```
			app.run(host='0.0.0.0', port=8000)
```
		  to
```
		  	app.run()
```
	10. Configure the PSQL  database to support the catalog project
	11. Added the new public domain url to my google key 
# List of third party resources used to complete this project:
	1. SSH
	2. Terminal
	3. AWS Lightsail web portal
	4. Udacity Forum
