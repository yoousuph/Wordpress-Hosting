# WORDPRESS WEBSITE HOSTING

# Introduction
This project demonstartes how Wordpres website is hosted on an EC2 instance conecting to  an RDS database. It is built in a Virtual Private Cloud(VPC) for isolated network connectivity.

# Project Overview
* Launched a separate VPC for isolted network in the AWS environment, in which there are 3 subnets.
    - 1 public subnet for the Wordpress server (EC2 iinstance).
    - 2 private subnets for the RDS which is reqired for the RDS subnet group.
* EC2 instance launch in the public subnet for internet connectivity to install required files.
* RDS instance launch as wordpress is required for connecting to a database.
* Setup Security groups for the services to talk to each other based on inbound and outbound rules.
* Create an internet gateway, routed to the public subnet where wordpress server will be situated.

# Technology Used
* Virtual Private Cloud (VPC)
* Elastic Compute Cloud (EC2)
* Relational Dtatabase Service (RDS)
* Internet gateway (IGW)

# Reference Architecture
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/wp-hosting-architecture.jpeg)

# Steps
**Setup a VPC**
* Create 1 VPC
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)
* Create 3 Subnets
![Project Screenshot 1.2.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.2.JPG)
* Create 1 Secondary Route Table
![Project Screenshot 1.3.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.3.JPG)
* Create 1 Internet Gateway
![Project Screenshot 1.6.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.6.JPG)

**Launch an EC2 Instance**
* Create 1 EC2 Instance - to host wordpress server
![Project Screenshot 1.7.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.7.JPG)
* Create a Key Pair - Keep for login purpose
![Project Screenshot 1.8.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.8.JPG)
* Create Security Group - Inbound & Outbound Rules
![Project Screenshot 1.10.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.10.JPG)

**Create an RDS Instance**
* Create 1 RDS Instance - to store database server
![Project Screenshot 1.9.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.9.JPG)
* Create Security Group - Inbound & Outbound Rules
![Project Screenshot 1.11.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.11.JPG)
* Create a Subnet Group - for the multi-AZ availability
![Project Screenshot 1.12.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.12.JPG)

**SSH into the wordpress EC2 instance (Using Putty in this case) and Update, and install Apache web server**
```bash
ec2-user@<your EC2 instance IPv4 address>
```
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.JPG)
```bash
sudo dnf update -y
sudo dnf install httpd -y
```
![Project Screenshot 1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.JPG)


**Start and enable Apache web server**
```bash
sudo systemctl start httpd
sudo systemctl enable httpd
```
![Project Screenshot 2.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/2.JPG)

**Confirm Apache web serving is running**
*Paste the IPv4 address of the EC2 instance on the web brower.*
![Project Screenshot 3.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/3.JPG)

**Install mysql client (Maria DB in this case)**
```bash
sudo dnf install -y mariadb105
```
![Project Screenshot 4.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/4.JPG)

**Log in to mysql client and create a database**
```bash
mysql -h wp-db.cibiocykye8k.us-east-1.rds.amazonaws.com -u admin -p
CRAETE DATABASE wordpress_db;
```
![Project Screenshot 5.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/5.JPG)

**Check current database to confirm the newly created database**
```bash
show databases;
```
![Project Screenshot 6.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/6.JPG)

**Create database user and give all priviledges of the database to the user**
```bash
CREATE USER 'yusuf'@'%' IDENTIFIED BY 'yusuf123';
GRANT ALL PRIVILEDGES ON wordpress_db.* TO 'yusuf'@'%';
FLUSH PRIVILEDGES;
exit;
```
![Project Screenshot 6.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/6.JPG)

**Test user login access**
```bash
mysql -h wp-db.cibiocykye8k.us-east-1.rds.amazonaws.com -u yusuf -p
```
![Project Screenshot 7.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/7.JPG)

**Install all PHP dependencies**
```bash
sudo dnf install php php-mysqlnd php-fpm php-gd php-xml php-mbstring php-json -y
```
![Project Screenshot 8.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/8.JPG)

**Change directory into html folder and download wordpress in it**
```bash
cd var/www/html
sudo wget https://wordpress.org/latest.tar.gz
sudo tar -xzf latest.tar.gz
```
![Project Screenshot 10.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/10.JPG)

**Move all the contents of extracted wordpress folder into the previous folder**

```bash
sudo mv wordpress/* .
sudo rm -rf wordpress latest.tar.gz
```
![Project Screenshot 10.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/10.JPG)

**Give administrative rights to apache server amd move all contents in wp-config-sample.php into new file wp-config.php**

```bash
sudo chown -R apache:apache /var/www/html
sudo chmod -R 755 apache:apache /var/www/html
sudo cp wp-config-sample.php wp-config.php
```
![Project Screenshot 9.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/9.JPG)

**Open wp-config file with any editor of your choice (nano in this case) and change info**
```bash
sudo nano wp-config.php

// ** MySQL settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define( 'DB_NAME', 'database_name_here' );

/** MySQL database username */
define( 'DB_USER', 'username_here' );

/** MySQL database password */
define( 'DB_PASSWORD', 'password_here' );

/** MySQL hostname */
define( 'DB_HOST', 'rds-endpoint-name' );
```

![Project Screenshot 13.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/13.JPG)

**Go to below link and it provides some information to update the wp-config file. It looks like below shared one.**
https://api.wordpress.org/secret-key/1.1/salt/
```bash
define('AUTH_KEY',         '+7CA?k*Ju&8eCfg=/aFKo0tO5Tn73Cg 9|Ed73k|Gw(3^');
define('SECURE_AUTH_KEY',  ':H$M&FvbE6t:EwH5ik/D!@]@%Dv3!-Q^hNH3*O+-$L6c*|');
define('LOGGED_IN_KEY',    'g9?;b_A BNW[; $9N^E2^jt$LkF 8_^baTmjhp<eE5GUd');
define('NONCE_KEY',        'G;Wf@|;jzQh>R812&-x^cPoq`tOOu>q)#JVa Y%No%.JpZ[');
define('AUTH_SALT',        'up^dE)4&x/?]1[thjghhjjhz6Vhiohr(dVMh+d5=R<.l_#l');
define('SECURE_AUTH_SALT', '@%ka=9?}BQ[m#29D+@jkgjkhjkhjkhkjhkjdTZ`MT{|fypE~');
define('LOGGED_IN_SALT',   'o!UX5|LW4eijhjkbhkjhkjkjbnjjb/1JSPS?e`YW*nrWb|FG ');
define('NONCE_SALT',       '+t}kH4DA`jhbjkbjkbjkbjkbjkbt8(iWX(]e?&tV;k:>|)IoE');
```
![Project Screenshot 11.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/11.JPG)

**Open the ip address of your server to the web browser**

You should see the image like this below - Else the your database configurations may need to be checked
![Project Screenshot 14.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/14.JPG)


**Configure your hosted wordpress website**

Fill all prefered informations as desired
![Project Screenshot 15.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/15.JPG)


**Login to the website**
![Project Screenshot 16.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/16.JPG)

**Your hosted website is ready**
![Project Screenshot 17.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/17.JPG)

# Conclusion
All highlighted in this project showcase my skills in deploying a wordpres website. It has helpd me understand the core concepts that are needed to successfully deploy a wordpress website on a separate EC2 instance.
