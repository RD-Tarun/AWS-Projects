# Creating and Hosting a Wordpress Server on AWS
---

This repository documents the process of setting up a WordPress server on AWS using an EC2 instance.

---

Creating a Wordpress Server using an EC2 instance

- Create an EC2 instance using the **Ubuntu** AMI.
- Select an instance type (e.g., t2.micro for free-tier usage).
- Configure security groups to allow SSH, HTTP, and HTTPS access.
- Launch the instance and connect to it using SSH.
 
Assigned elastic IP to the instance because the IP needs to be static and not change everytime I try to connect to it.

![image](https://github.com/user-attachments/assets/693c64c8-74a0-445d-a7f2-1d9abe886541)

---

Using a SSH Client, connected to the Ubuntu Machine

![image](https://github.com/user-attachments/assets/3027a4d2-0bf8-43e7-a077-6f553a226fbd)

![image](https://github.com/user-attachments/assets/bd2d394a-8108-41f2-85c4-b824237f4f6c)

---

Created an apache server for the Elastic IP using 
```bash
sudo apt install apache2
```
![image](https://github.com/user-attachments/assets/7a2c6a70-e044-47c5-b6f1-af3949372e65)

---

Configured the mySQL authentication plugin to a mySQL native password inorder to login into the server with a normal password

![image](https://github.com/user-attachments/assets/bc35e48f-0af2-4c49-a23c-82531ca51ac2)

---

Downloaded WordPress Installer from the web and extracted it.

![image](https://github.com/user-attachments/assets/5c34ea02-6047-4925-8150-156c9d169e53)

---

After logging into Wordpress, configured the *wp-config.php* file.
![image](https://github.com/user-attachments/assets/1deb4fa2-7b9c-4a32-b011-ee2e7548ee76)

---

Logged in with the corresponding credentials
![image](https://github.com/user-attachments/assets/3c59f8a7-d474-4719-9107-44dc26dcf4fd)

---

Now, opening the website with the IP Address, we get:
![image](https://github.com/user-attachments/assets/0ca5b5ae-3af5-4b5f-89b2-dd1b89628add)

Changed the configuration such that I do not want the application in the URL, so now it just comes when I give the IP itself.
![image](https://github.com/user-attachments/assets/8f908e56-1b8c-46ce-8118-db55601386b6)

---
The Result:

![image](https://github.com/user-attachments/assets/0bcd3a2f-3c8f-416b-8b3c-38c3f458c2bc)

