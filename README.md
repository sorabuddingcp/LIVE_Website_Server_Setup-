# LIVE_Website_Server_Setup-
LIVE Website Server Setup Manual

---------------------Start-------------------

LIVE Website Server Setup Manual
Version 1.0

This is a step by step guide to setup server and environment for LIVE Website Server
Prerequisite:
•	Distribution Server Version – Ubuntu 20.04
•	Service name: –  Linux, Apache2, PHP 7.4, MYSQL 5.6
Wildcard ssl with domain : If local configure then need entry host name for LIVE Website Server
•	
Setup of Instance containing business logic –
1.	Environment requirement – Linux(Ubuntu20), Apache(v2.4.41), php(version 7.43)
2.	Need server root access
3.	Environment Setup: Apache –
a.	sudo apt -get update 
b.	sudo apt -get install apache2
c.	(Create iot user) sudo useradd -s /bin/bash -d /home/example/ -m -G sudo example
d.	Set up sudo password: sudo passwd example
e.	(Create Example directory ) sudo mkdir -p /home/example/public
f.	(Change Example Directory  permission):                                                                                        sudo chown example: example  /home/example/public
g.	(Firewall Update) sudo ufw app list
h.	(Firewall allow apache) sudo ufw allow in "Apache"
i.	(Firewall Status check) sudo ufw status
j.	(copy the IP address and past web browser check apache default page open If apache default page does not open then check firewall)  >>http:// 127.0.0.1 (your server ip address)
4.	Environment Setup: php  –  
a.	(Install PHP) sudo apt install php libapache2-mod-php php-mysql
b.	php -v
c.	(php 7.4 extensions) sudo apt install php-cli php-fpm php-json php-common php-mysql php-zip php-gd php-mbstring php-curl php-xml php-pear php-bcmath

5.	Environment Setup: Creating virtual host – 

a.	(Creating a Virtual Host for your Website)
b.	(Example configure file ) -(Go to below path)-> Path: /etc/apache2/sites-available/000-default.conf
c.	(Copy virtual host configure file ): Sudo cp /etc/apache2/sites-available/000-default.conf  /etc/apache2/sites-available/ example.conf  
d.	Vim /etc/apache2/sites-available/ example.conf 

Change project path:
<VirtualHost *:80>
        # The ServerName directive sets the request scheme, hostname and port that
        # the server uses to identify itself. This is used when creating
        # redirection URLs. In the context of virtual hosts, the ServerName
        # specifies what hostname must appear in the request's Host: header to
        # match this virtual host. For the default virtual host (this file) this
        # value is not decisive as it is used as a last resort host regardless.
        # However, you must set it for any further virtual host explicitly.
        #ServerName www.example.com

ServerAdmin webmaster@localhost
 DocumentRoot /home/ example/public
 ServerName  example.live
 ServerAlias *.example.live
 ErrorLog ${APACHE_LOG_DIR}/error.log
 CustomLog ${APACHE_LOG_DIR}/access.log combined

<Directory /home/example/public >
Options Indexes FollowSymLinks
   AllowOverride all
      Require all granted
   </Directory>

        # Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
        # error, crit, alert, emerg.
        # It is also possible to configure the loglevel for particular
        # modules, e.g.
        #LogLevel info ssl:warn

        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined

        # For most configuration files from conf-available/, which are
        # enabled or disabled at a global level, it is possible to
        # include a line for only one particular virtual host. For example the
        # following line enables the CGI configuration for this host only
        # after it has been globally disabled with "a2disconf".
        #Include conf-available/serve-cgi-bin.conf
</VirtualHost>

•	(For vim save ) # wq!

Enable virtual host:
a) sudo a2ensite example.conf  
b) sudo systemctl reload apache2
6.	Environment test –
a.	 vim /home/example/public/info.php
b.	<?php phpinfo(); ?>
c.	(Check php info.php) 
d.	(http://server_domain_or_IP/info.php ). 127.0.0.1/info.php (Your ip address/info.php)



     7.if you does not live domain then needs entry host name in your local system.

a.	Go to run  open cmd with administrator
b.	Cd drivers
c.	Cd etc
d.	Notepad host  



e.	entry your main domain and sub-domian in host file
#	127.0.0.1       localhost
#	::1             localhost
Yourserverip       yourdamin
34.76.203.197	   domain name


  
Find the IP address and default page:
 
•	Compete Engine -->VM Instances -->External IP (Your server IP)
•	Ipconfig (show your local ip address)

OR 

To find your public IP addresses, use the opendns.com resolver as in the command below In Server :

•	$ dig +short myip.opendns.com @resolver1.opendns.com

Setup of MSQY same server database –
Step 1 :
Step 1 — Installing MySQL
•	sudo apt update
•	sudo apt install mysql-server
•	sudo systemctl start mysql.service
•	
Step 2 — Configuring MySQL
•	sudo mysql_secure_installation
•	Please enter 0 = LOW, 1 = MEDIUM and 2 = STRONG:
•	 2
•	Please set the password for root here.
•	New password:
•	Re-enter new password:
Step 3 — Creating a Dedicated MySQL User and Granting Privileges
•	sudo mysql
•	mysql -u root -p
•	
•	CREATE USER 'example'@'localhost' IDENTIFIED BY 'Eiqrcokiz5%';
•	GRANT ALL ON example_db.* TO 'example'@'localhost';
•	
•	create database example_db;
•	
•	flush privileges;FLUSH PRIVILEGES;

Step 4 — Importing a MySQL Database
•	mysql -u root -p
•	CREATE DATABASE example_db;
•	mysql -u username -p new_example_db < example_db_backup.sql
•	
Optional You can user PHPMYADMIN for database importing
•	Sudo apt-get install phpMyAdmin
•	Localhost/phpmyadmin
•	Your ip address/phpmyadmin

Project File Upload:
•	Go to /home/example/public
•	(QR-code download) wget https://example.live/example_backup.zip
•	Unzip example_backup.zip
Application database configure:
•	Go to /home/example/public
•	Vim public/application/config/database.php
Change application database credentials:-
o	$db['default'] = array(
o	'dsn'   => '',
o	'hostname' => 'localhost',
o	'username' => 'example',
o	'password' => 'Eiexampleuiz5%',
o	'database' => 'example_db',
o	'dbdriver' => 'mysqli',



Environment test 
•	Super Admin application test -  
o	URL: http:// your mail domain (example.com)
o	User Name: admin@gmail.com
o	Password: 123456
•	Restaurant Admin application test –
o	URL: http:// your sub-domain (alibaba.example.com)
o	User Name: restaurant@gmail.com
o	Password: 123456





End…
