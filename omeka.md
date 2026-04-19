## Installing Omeka
This is the process of adding omeka to my vm to work with Wordpress.
### Step One: 
Create a database and a user

```bash
sudo mysql -u root

then:
```bash
create user 'wordpress'@'localhost' identified by 'c';
create database wordpress;
grant all privileges on wordpress.* to 'wordpress'@'localhost';
show databases;
\q

### Download Omeka

```bash
wget https://github.com/omeka/Omeka/releases/download/v3.2/omeka-3.2.zip
sudo unzip omeka-3.2.zip

### Enter Login Information
user: 
password:
