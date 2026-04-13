# Wordpress Install
## Objective of installing Wordpress to create a functioning site.
## Steps Taken:
## Step one: check for current versions of php
ran: php --version and then
mysql --version
both tests okay
ran command:
sudo apt install php-curl php-xml php-imagick php-mbstring php-zip php-intl
Then restartedd Apache2 and MySQL:
Ran: sudo systemctl restart apache2
Ran: sudo systemctl restart mysql
everything was fine
## Step two:
Continued with installation by running:
cd /var/www/html
sudo wget https://wordpress.org/latest.zip
sudo unzip latest.zip
To create a user I did the following
ran: sudo mysql -u root -p 
typed in the password
then ran the command:
create user 'wordpress'@'localhost' identified by '123456c@TS';
create database wordpress;
grant all privileges on wordpress.* to 'wordpress'@'localhost';
show databases;
\q
## Step three:
Configed the php file by running 
cd /var/www/html/wordpress
sudo cp wp-config-sample.php wp-config.php
sudo nano wp-config.php

The process was pretty straightforward and it was neat to see an immediate chance in the web address so soon after installation. 
