# Update the system packages
sudo yum update -y
clear

# Install Apache (httpd), MariaDB, and PHP
sudo yum install httpd mariadb105-server php -y

# Download and extract WordPress
sudo wget https://wordpress.org/latest.tar.gz
sudo tar -xvzf latest.tar.gz
ls

# Move WordPress to the web directory
sudo mv wordpress /var/www/html/

# Start the services
sudo systemctl start httpd
sudo systemctl start mariadb
sudo systemctl start php-fpm

# Change directory to web root
cd /var/www/html/

# Install PHP MySQL extension
sudo yum install php8.4-mysqlnd.x86_64

# Access MySQL shell
sudo mysql
sudo mysql -u root -p

# Create the WordPress database inside MySQL shell
create database your_database_name;

# Set permissions for WordPress directory
cd /var/www/html/
sudo chmod -R 777 /var/www/html/wordpress
ls -l

# Open FTP ports (20–21) in the security group of your cloud provider for access to the public IP

# Install and configure FTP server
sudo yum install vsftpd -y
sudo useradd vsftp
sudo passwd vsftp

# Check permissions
ls -l

# Start FTP service
sudo systemctl start vsftpd

# Adjust ownership for WordPress files
sudo chown vsftp /var/www/html/wordpress
sudo chgrp apache /var/www/html/wordpress
ls -l
