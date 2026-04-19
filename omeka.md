## Installing Omeka
This is the process of adding omeka to my vm to work with Wordpress.
### Step One: 
Create a database and a user

```bash
sudo mysql -u root

then:
```bash
create user 'omeka'@'localhost' identified by '123456c@TS';
create database omeka;
grant all privileges on omeka.* to 'omeka'@'localhost';
show databases;
\q

### Download Omeka

```bash
wget https://github.com/omeka/Omeka/releases/download/v3.2/omeka-3.2.zip
sudo unzip omeka-3.2.zip

### Enter Login Information
user: omeka
password: 123456c@TS

##
