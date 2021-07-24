# LEMP STACK IMPLEMENTATION
## INSTALLING THE NGINX WEBSERVER
#### Nginx, a high-performance web server will be used to display our pages as we begin with updates
* sudo apt update
![Update](https://user-images.githubusercontent.com/51024695/126869861-b5351b64-2e8b-4c1a-83c6-46150aafb4a2.PNG)
* sudo apt install nginx
#### Type Y to confirm installation when promted.
#### Verify that nginx installed successfully.
* sudo systemctl status nginx
![nginx confirmation](https://user-images.githubusercontent.com/51024695/126869971-2b1e39d5-a9c7-4ff5-b758-570429915e33.PNG)
#### We need to open TCP port 80 to allow web traffic so edith the inbound rules to reflect this.
#### Rest Nginx on port 80 using curl or IP curl dns name
* curl http://localhost:80
* curl http://127.0.0.1:80
![curl check](https://user-images.githubusercontent.com/51024695/126870162-ecf92530-0bc3-489a-b4d7-96deaa7baeae.PNG)
![curl ip](https://user-images.githubusercontent.com/51024695/126870163-7720ee61-611e-4ba6-9893-966afaab9636.PNG)
#### Open nginx on web browser, It should work whether or not you specify port number
* http://<Public-IP-Address>🈵
![nginx webpage](https://user-images.githubusercontent.com/51024695/126870502-a0b80e4d-ee27-4b2b-ba49-443ad407ecb0.PNG)
## Installing MySQL
![SQL install](https://user-images.githubusercontent.com/51024695/126870653-05dcb2e2-0609-425d-bb03-68e7488e61be.PNG)
#### Run sql secure installation
* sudo mysql_secure_installation
#### If you choose to use validate password be sure to meet the password criteria when entering password otherwise it will be rejected
#### Enter Y for yes or anything else to continue installation.You may skip this process as it is a test enviroment
#### In a Production enviroment, this decision may not be for you to take.
#### Login to mysql
* sudo mysql
![SQL LOGIN](https://user-images.githubusercontent.com/51024695/126871040-c9d36912-6f10-486e-8849-53a21ab0074a.PNG)
## Installing PHP
#### You need to install php-fpm and php-mysql, use the command below to install both packages
* sudo apt install php-fpm php-mysql
#### Type Y and hit ENTER key when prompted to complete installation
## Configuring Nginx to Use PHP Processor
#### we will use projectLEMP as an example domain name.
* sudo mkdir /var/www/projectLEMP
#### Change ownership of the directory with the $USER environment variable, which will reference your current system user
* sudo chown -R $USER:$USER /var/www/projectLEMP
#### open a new configuration file in Nginx’s sites-available directory using nano editor
* sudo nano /etc/nginx/sites-available/projectLEMP
#### copy the bar-bone config below and paste
![barebone confirmation](https://user-images.githubusercontent.com/51024695/126872396-c0e0b344-9e00-4d93-a835-ad8e2f1625c1.PNG)
#### To Activate your configuration, link to the config file from Nginx’s sites-enabled directory
* sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/
#### Test nginx for configuration errors
* sudo nginx -t
![nginx syntax test](https://user-images.githubusercontent.com/51024695/126873872-9f33d63a-ba24-4880-8f21-3774a0625aee.PNG)
#### Run the command below to disable default Nginx host set to listen on port 80
* sudo unlink /etc/nginx/sites-enabled/default
#### Reload Nginx
* sudo systemctl reload nginx
![nginx enable and reload](https://user-images.githubusercontent.com/51024695/126874166-a1d5cd34-5614-463f-bfb6-f8ecb1acc6b0.PNG)
#### At this point the website is active but root directory is still empty
* sudo echo 'Hello LEMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectLEMP/index.html
#### Now go to your type the public ip of webserver, launch another tab and type public dns of your server
![nginx web IP confirm page](https://user-images.githubusercontent.com/51024695/126874322-0a3bd613-4e8c-4216-9b4e-5347c7e7d639.PNG)
![nginx web DNS confirm page](https://user-images.githubusercontent.com/51024695/126874326-a7f9b7f1-0ae2-4f1e-97e9-7a967def941e.PNG)
## Testing PHP with Nginx
#### Create a PHP test file in the root called info.php
* sudo nano /var/www/projectLEMP/info.php
#### Type the following 
<?php
phpinfo();
#### Now access this page in your web browser by visiting the domain name or public IP address
![info php](https://user-images.githubusercontent.com/51024695/126874789-bf042c09-da09-4d7e-b235-15838ef81b25.PNG)
## Retrieving data from MySQL database with PHP
#### First, connect to the MySQL console using the root account
* sudo mysql
#### Create a database
* CREATE DATABASE `example_database`;
![CREATING EXAMPLE DATABASE](https://user-images.githubusercontent.com/51024695/126875015-0914b711-4fdb-4287-a5e9-6e7700e93efe.PNG)
#### Create a new user and grant him full privileges on the database
* CREATE USER 'example_user'@'%' IDENTIFIED WITH mysql_native_password BY 'password';
![sql user password](https://user-images.githubusercontent.com/51024695/126875067-0e8d16d7-f316-4c7c-a317-3ce653ed1ea9.PNG)
![sql user permission](https://user-images.githubusercontent.com/51024695/126875033-a13303e0-e41f-467f-89f5-c172d4616164.PNG)
#### Exit the MySQL shell with exit command
#### Test if the new user has the proper permissions by logging in to the MySQL console again
* mysql -u example_user -p
* SHOW DATABASES;
![access to database](https://user-images.githubusercontent.com/51024695/126875242-17d96477-64eb-4954-ae07-7ac8db0c998c.PNG)

  
  
