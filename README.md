# AWS Projects

### A comprehensive collection of projects that demonstrate the use of Amazon Web Services (AWS) across various domains and technologies. Each project showcases specific AWS services, architecture designs, and implementation strategies to demonstrate my expertise in using AWS Services.

---

## 1. Exponentiation Calculator
A serverless web application that computes mathematical exponentiation of a base and its exponent.

### Services Used: AWS Lambda, API Gateway, DynamoDB, Amplify, and IAM.

#### Highlights:
- **Fully Serverless Architecture**: Ensures cost efficiency and scalability.
- **API Gateway**: Enables seamless communication between frontend and backend.
- **DynamoDB**: Stores computation results with timestamps for future reference.
- **AWS Amplify**: Manages frontend deployment and hosting.
- **IAM Policies**: Ensure secure access to resources.

This project demonstrates how to build and deploy a serverless application for a mathematical use case while leveraging AWS services for backend computation, storage, and security.

---

## 2. Creating and Hosting a WordPress Server on AWS
Setting up and hosting a WordPress server on AWS, leveraging Elastic IPs and robust server configurations to ensure reliability and accessibility.

### Services Used: AWS EC2, Apache, MySQL, WordPress, Elastic IP.

#### Highlights:
- **EC2 Instance Setup**: 
  - Launched an Ubuntu-based EC2 instance (e.g., t2.micro for free-tier usage).
  - Configured security groups to allow SSH, HTTP, and HTTPS access.
- **Elastic IP**: 
  - Assigned a static Elastic IP to the instance for consistent connectivity.
- **Apache Web Server**: 
  - Installed and configured Apache:
    ```bash
    sudo apt install apache2
    ```
- **MySQL Configuration**: 
  - Updated MySQL authentication to use a native password plugin for straightforward database management.
- **WordPress Installation**: 
  - Downloaded and extracted the WordPress installer.
  - Configured the `wp-config.php` file to connect WordPress to the MySQL database.
- **URL Simplification**: 
  - Modified server settings to enable direct website access via the Elastic IP without additional URL paths.
- **Website Deployment**: 
  - Successfully deployed WordPress, allowing access to the site and admin panel via the IP address.

### Final Result:
- WordPress site accessible via the Elastic IP.
- Fully functional admin panel for managing the site.

---
