## Koha Install
### Step One
`bash
sudo apt install tmux ;
after sucessfully installing make sure the system us up to date with
`bash
sudo apt update
sudo apt upgrade
sudo apt autoremove -y && sudo apt clean

### Step Two
Add Koha repository 
`bash
sudo apt install apt-transport-https ca-certificates curl ;
`bash
sudo mkdir -p --mode=0755 /etc/apt/keyrings ;
`bash
sudo curl -fsSL https://debian.koha-community.org/koha/gpg.asc -o /etc/apt/keyrings/koha.asc
`bash
sudo su
`bash
tee /etc/apt/sources.list.d/koha.sources <<EOF
Types: deb
URIs: https://debian.koha-community.org/koha/
Suites: 25.05
Components: main
Signed-By: /etc/apt/keyrings/koha.asc
EOF

`bash
exit

### Step Three Add Maria DB
`bash
sudo apt update
`bash
sudo apt install mariadb-server

### Step Four Install Koha
`bash 
sudo apt update
`bash
apt show koha-common
`bash 
sudo apt install koha-common

### Step Five Open Ports
`bash 
sudo cp /etc/koha/koha-sites.conf /etc/koha/koha-sites.conf.backup
`bash
sudo nano /etc/koha/koha-sites.conf
At the end of the INTRAPORT= line, add 8080. At the end of the OPACPORT= line, add 8081:

### Step Six Set Up Apache
`bash
sudo a2enmod rewrite cgi headers proxy_http
sudo systemctl restart apache2
`bash
sudo cp /etc/apache2/ports.conf /etc/apache2/ports.conf.backup
`bash
sudo nano /etc/apache2/ports.conf. 
Under Listen 80 at the top of the file, add the following two lines: Listen 8080 Listen 8081

### Step Seven Create Koha Instance
`bash
sudo koha-create --create-db bibliolib
sudo systemctl restart apache2

### Step Eight Apache2 Config
` bash
sudo a2dissite 000-default
sudo a2enmod deflate
sudo a2ensite bibliolib

`bash
sudo systemctl reload apache2
sudo systemctl restart apache2

`bash
sudo systemctl reload apache2
sudo systemctl restart apache2

### Step Nine Koha Web Installer
`bash
sudo systemctl reload apache2
sudo systemctl restart apache2
`bash
sudo koha-passwd bibliolib


### Step Ten Admin config
`bash
http://104.154.60.53:8080
