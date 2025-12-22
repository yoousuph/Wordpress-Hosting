# WORDPRESS WEBSITE HOSTING

# Architecture
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/wp hosting architecture.jpeg)

# Introduction
This project demonstartes hosting of a wordpress website on an EC2 istance conecting with a Database using RDS Database Instance. It is built in an isolated Virtual Private Cloud(VPC) form scratch.

# Tech Stack
**AWS Services Used**
* Virtual Private Cloud (VPC)
* Elastic Compute Cloud (EC2)
* Relational Dtatabase Service (RDS)

# Procedure
**Setup a VPC**
* Create 1 VPC
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)
* Create 3 Subnets
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)
* Create 1 Secondary Route Table
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)
* Create 1 Internet Gateway
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)

**Launch an EC2 Instance**
* Create 1 EC2 Instance - to host wordpress server
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)
* Create a Key Pair - Keep for login purpose
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)
* Create Security Group - Inbound & Outbound Rules
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)

**Create an RDS Instance**
* Create 1 RDS Instance - to store database server
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)
* Create Security Group - Inbound & Outbound Rules
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)
* Create a Subnet Group - for the multi-AZ availability
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)


```bash
sudo dnf update -y
```
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)

**Update the EC2 instance**
```bash
sudo dnf update -y
```
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)

**Install Apache web server**
```bash
sudo dnf install httpd -y
```
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)

**Start and enable Apache web server**
```bash
sudo systemctl start httpd
sudo systemctl enable httpd
```
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)

**Install mysql server**
```bash
sudo dnf install -y mariadb105
```
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)

**Log in to mysql client**
```bash
mysql -h wp-db.cibiocykye8k.us-east-1.rds.amazonaws.com -u admin -p
```
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)

**Check default current database**
```bash
show databases;
```
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)

**Create a database for you wordpress website**
```bash
CRAETE DATABASE wordpress_db;
```
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)

**Check current database to confirm the newly created database**
```bash
show databases;
```
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)

**Create database user**
```bash
CREATE USER 'yusuf'@'%' IDENTIFIED BY 'yusuf123';
```
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)

**Grant database user access to the database**
```bash
GRANT ALL PRIVILEDGES ON wordpress_db.* TO 'yusuf'@'%';
```
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)

**Flush priviledges**
```bash
FLUSH PRIVILEDGES;
```
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)

**Test user login access**
```bash
mysql -h wp-db.cibiocykye8k.us-east-1.rds.amazonaws.com -u yusuf -p
```![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)

**Install all PHP dependencies**
```bash
sudo dnf install php php-mysqlnd php-fpm php-gd php-xml php-mbstring php-json -y
```
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)

**Install all PHP dependencies**
```bash
sudo dnf install php php-mysqlnd php-fpm php-gd php-xml php-mbstring php-json -y
```
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)

**Restart and enable Apache web server**
```bash
sudo systemctl restart httpd
```
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)

**Change directory into html folder**
```bash
cd var/www/html
```
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)

**Download wordpress inside html folder and unzip it**
```bash
sudo wget https://wordpress.org/latest.tar.gz
sudo tar -xzf latest.tar.gz
```
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)

**Download wordpress inside html folder and unzip it**
```bash
sudo wget https://wordpress.org/latest.tar.gz
sudo tar -xzf latest.tar.gz
```
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)

**Move all the contents of extracted wordpress folder into the previous folder**
```bash
sudo mv wordpress/* .
```
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)

**Remove the emptyed wordpress folder and the downloaded zip file from the folder**
```bash
sudo rm -rf wordpress latest.tar.gz
```
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)

**Give administrative rights to apache server**
```bash
sudo chown -R apache:apache /var/www/html
sudo chmod -R 755 apache:apache /var/www/html
```
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)

**Move all contenets in wp-config-sample php file into a new wp-config file**
```bash
sudo cp wp-config-sample.php wp-config.php
```
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)

**Open thw w-config file with any editor of your choice (nano in this case)**
```bash
sudo nano wp-config.php
```
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)

**Replace the Database_name_here , "username_here", "password_here" and "rds-endpoint-name" with valid info**

```bash
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
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)

**Go to below link and it provides some information to update the wp-config file. It looks like below shared one.**

```bash
https://api.wordpress.org/secret-key/1.1/salt/
```
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)

**Acquire the valid information and update wp-config file accordingly**

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
![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)

**Open the ip address of your server to the web browser**

![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)


**Configure your hosted wordpress website**

![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)


**Login to the website**

![Project Screenshot 1.1.JPG](https://github.com/yoousuph/Wordpress-Hosting/blob/main/images/1.1.JPG)














