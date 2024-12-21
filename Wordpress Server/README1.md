# Creating and Hosting a WordPress Server on AWS

This repository documents the process of setting up a WordPress server on AWS using an EC2 instance. The guide also includes the necessary steps to configure Apache, MySQL, and WordPress, ensuring a static IP for the server with an Elastic IP.

## Prerequisites

1. An AWS account with access to create EC2 instances.
2. Basic knowledge of Linux commands.
3. Security groups configured to allow HTTP (port 80) and HTTPS (port 443) access.

## Steps to Setup WordPress on AWS

### 1. Launch an EC2 Instance

- Create an EC2 instance using the **Ubuntu** AMI.
- Select an instance type (e.g., t2.micro for free-tier usage).
- Configure security groups to allow SSH, HTTP, and HTTPS access.
- Launch the instance and connect to it using SSH.

### 2. Assign an Elastic IP

- Go to the **Elastic IP** section in the AWS Management Console.
- Allocate a new Elastic IP and associate it with your EC2 instance.
- This ensures that the IP address remains static and does not change after reboots.

### 3. Update the System

```bash
sudo apt update && sudo apt upgrade -y
```

### 4. Install Apache Server

```bash
sudo apt install apache2 -y
```

- Enable and start the Apache service:

```bash
sudo systemctl enable apache2
sudo systemctl start apache2
```

### 5. Install MySQL

```bash
sudo apt install mysql-server -y
```

- Secure the MySQL installation:

```bash
sudo mysql_secure_installation
```

- Configure MySQL to use the native password authentication plugin:

```bash
sudo mysql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'your_password';
FLUSH PRIVILEGES;
EXIT;
```

### 6. Install PHP

```bash
sudo apt install php libapache2-mod-php php-mysql -y
```

### 7. Download and Install WordPress

- Download the latest WordPress package:

```bash
wget -c https://wordpress.org/latest.tar.gz
```

- Extract the package and move it to the Apache web directory:

```bash
tar -xvzf latest.tar.gz
sudo mv wordpress /var/www/html/
```

- Set permissions for the WordPress directory:

```bash
sudo chown -R www-data:www-data /var/www/html/wordpress
sudo chmod -R 755 /var/www/html/wordpress
```

### 8. Configure Apache for WordPress

- Create a new Apache configuration file for WordPress:

```bash
sudo nano /etc/apache2/sites-available/wordpress.conf
```

Add the following configuration:

```apache
<VirtualHost *:80>
    ServerAdmin admin@example.com
    DocumentRoot /var/www/html/wordpress
    ServerName yourdomain.com

    <Directory /var/www/html/wordpress>
        Options FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

- Enable the configuration and rewrite module:

```bash
sudo a2ensite wordpress.conf
sudo a2enmod rewrite
sudo systemctl restart apache2
```

### 9. Setup MySQL Database for WordPress

- Log in to MySQL:

```bash
sudo mysql -u root -p
```

- Create a database and user for WordPress:

```sql
CREATE DATABASE wordpress;
CREATE USER 'wordpressuser'@'localhost' IDENTIFIED BY 'your_password';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wordpressuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

### 10. Complete WordPress Installation

- Access your WordPress installation via your browser:

```
http://your-elastic-ip
```

- Follow the on-screen setup wizard to configure your WordPress site.

## Screenshots

Include screenshots showcasing:

1. EC2 instance setup.
2. Elastic IP assignment.
3. Apache and MySQL configuration.
4. WordPress installation.

## Troubleshooting

- Ensure the security group allows inbound traffic on ports 80 and 443.
- Check Apache and MySQL service statuses:

```bash
sudo systemctl status apache2
sudo systemctl status mysql
```

- Review Apache logs for errors:

```bash
sudo tail -f /var/log/apache2/error.log
```

## License

This project is licensed under the MIT License. See the LICENSE file for details.
