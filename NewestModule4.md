# LAMP Stack Installation on Google Cloud VM

This document describes my experience setting up a LAMP stack on a
virtual machine (VM) hosted on Google Cloud.

## What is a LAMP Stack?

A LAMP stack consists of:

-   **Linux** -- Operating system\
-   **Apache** -- Web server\
-   **MySQL** -- Database server\
-   **PHP** -- Server-side scripting language

The goal of this project was to install, configure, and verify that all
components work together as a functional web stack.

------------------------------------------------------------------------

## Step 1: System Update

Before installing any software, I updated the package list:

``` bash
sudo apt update
```

This completed successfully with no errors.

------------------------------------------------------------------------

## Step 2: Install Apache

``` bash
sudo apt install apache2
```

Verify Apache is running:

``` bash
systemctl status apache2
```

**Expected output:**

    Active: active (running)

------------------------------------------------------------------------

## Step 3: Test Apache

Install a text-based browser:

``` bash
sudo apt install elinks
```

Navigate to:

    http://34.75.80.108/

The default Apache page displayed correctly.

------------------------------------------------------------------------

## Step 4: Create a Webpage

``` bash
cd /var/www/html/
sudo mv index.html index.original.html
sudo nano index.html
```

Add the following HTML:

``` html
<html>
<head>
<title>My first web page using Apache</title>
</head>
<body>
<h1>Welcome</h1>
<p>Welcome to my web site.
I created this site using the Apache HTTP server.</p>
</body>
</html>
```

Test:

    http://34.75.80.108/index.original.html

------------------------------------------------------------------------

## Step 5: Install PHP

``` bash
sudo apt install php libapache2-mod-php
sudo systemctl restart apache2
```

Check PHP version:

``` bash
php -v
```

------------------------------------------------------------------------

## Step 6: Test PHP

``` bash
cd /var/www/html/
sudo nano info.php
```

Add:

``` php
<?php
phpinfo();
?>
```

Open in browser:

    http://34.75.80.108/info.php

After verifying, remove the file for security:

``` bash
sudo rm /var/www/html/info.php
```

------------------------------------------------------------------------

## Step 7: Configure Apache

``` bash
cd /etc/apache2/mods-available/
sudo cp dir.conf dir.conf.bak
sudo nano dir.conf
```

Update to:

    DirectoryIndex index.php index.html

Test configuration:

``` bash
apachectl configtest
```

------------------------------------------------------------------------

## Step 8: Create PHP Application

``` bash
cd /var/www/html/
sudo nano index.php
```

Add:

``` php
<?php
$user_agent = $_SERVER['HTTP_USER_AGENT'];

if (stripos($user_agent, 'Chrome') !== false) {
    $browser = 'Google Chrome';
} else {
    $browser = 'Unknown Browser';
}

echo "<p>Your browser is <strong>$browser</strong>.</p>";
?>
```

Test:

    http://34.75.80.108/

------------------------------------------------------------------------

## Step 9: Install MySQL

Update system:

``` bash
sudo apt update
sudo apt upgrade
sudo apt autoremove
sudo apt clean
```

Install MySQL:

``` bash
sudo apt install mysql-server
```

Verify installation:

``` bash
mysql --version
systemctl status mysql
```

------------------------------------------------------------------------

## Step 10: Secure MySQL

``` bash
sudo mysql_secure_installation
```

Follow prompts as instructed.

------------------------------------------------------------------------

## Step 11: Access MySQL

``` bash
sudo mysql -u root
```

Run:

``` sql
SHOW DATABASES;
```

------------------------------------------------------------------------

## Errors & Troubleshooting

### SQL Syntax Error

    ERROR 1064 (42000)

-   **Cause:** Incorrect command input\
-   **Fix:** Re-enter command carefully

### MySQL Service Failure

-   **Error:** MySQL service failed to start\
-   **Cause:** VM performance issues\
-   **Fix:** Ran updates again and restarted services

------------------------------------------------------------------------

## Conclusion

The LAMP stack was successfully installed and configured. Apache served
web pages, PHP executed scripts, and MySQL handled database operations.
All components worked together as expected.

## Skills Gained

-   Linux command line\
-   Web server configuration\
-   PHP integration\
-   Database setup and security\
-   Troubleshooting system issues
