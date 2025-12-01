# Website Hosting on AWS EC2 — Complete Theory + Steps

* This guide explains the complete theory and practical steps to host a website on Amazon EC2 using Apache Web Server.<br>
* Perfect for DevOps, Cloud, and AWS learning projects.

# 1. Introduction

Website hosting means placing your website files (HTML, CSS, JS, images) on a server so the public can access them over the internet.

AWS EC2 (Elastic Compute Cloud) provides a virtual machine where you can:

* Install a web server

* Deploy website files

* Access it via Public IP or domain

* Fully control the OS, networking, and security

This project demonstrates hosting a static website using Amazon Linux 2 EC2 instance.

# Important Concepts 

* ###  EC2 Instance
  A virtual server in the cloud where you run applications.

* ### AMI (Amazon Machine Image)

  A preconfigured OS image (Linux, Windows).
  We use Amazon Linux 2.

* ### Instance Type

  Defines CPU, memory, network performance.
  Use: t2.micro (Free Tier).

* ### Key Pair

  SSH private key (.pem) used to securely log in to EC2.

* ### Security Groups

  A virtual firewall that controls inbound/outbound traffic.

  Required rules:

     | Type | Port | Description    |
     | ---- | ---- | -------------- |
     | SSH  | 22   | Login to EC2   |
     | HTTP | 80   | Website access |

* ### Web Server

  Software that serves web pages.
  Example: Apache (httpd), NGINX.

  We use: Apache Web Server.

* ### Document Root

  Location where website files are stored:<br>
  /var/www/html

* ### Architecture Diagram

  User Browser ---> HTTP (Port 80) ---> EC2 Instance ---> Apache Server ---> Website Files

# Step-by-Step Implementation
###  Step 1: Login to AWS

  Go to AWS Console → Search for EC2.

###  Step 2: Launch EC2 Instance

* Click Launch Instance

* Name: Website-Hosting-Server

* AMI: Amazon Linux 2

* Instance Type: t2.micro

* Create Key Pair: download .pem file

* Security Group:

      * Allow SSH (22) → My IP

      * Allow HTTP (80) → 0.0.0.0/0

Click Launch Instance

### Step 3: Connect to EC2
  
### Option A — EC2 Instance Connect

* Select instance

* Click Connect

* Open EC2 Instance Connect

### Option B — SSH (PowerShell/CMD)

    ssh -i "your-key.pem" ec2-user@<Public-IP>

### Step 4: Update Server Packages
    
    sudo yum update -y

### Step 5: Install Apache Web Server
    
    sudo yum install httpd -y

### Start Apache:

    sudo systemctl start httpd
    sudo systemctl enable httpd

### Check the service:

    sudo systemctl status httpd

#   Step 6: Deploy Website
### Go to Apache document root:
   
    cd /var/www/html

### Create homepage:
    
    sudo nano index.html

### Add sample content:

    <h1>Welcome to My Website Hosted on AWS EC2</h1>
    <p>This server is running on Apache Web Server.</p>

# Step 7: Test the Website

### Open browser → Enter EC2 Public IP:

    http://<your-ec2-ip>

  You should see your webpage live.

  5. Useful Commands

### Restart Apache:

    sudo systemctl restart httpd

### Check open ports:

    sudo ss -tulpn | grep httpd

### View IP:

    curl ifconfig.me

# 6. Summary

* This project demonstrates:

* Launching an EC2 instance

* Configuring security groups

* Installing Apache web server

* Deploying website files

* Accessing the site via Public IP

## This is the foundation for further cloud projects like:

* Hosting dynamic websites

* Using Elastic IP

* Using Load Balancers

* Using Auto Scaling

* Hosting with NGINX

* CI/CD deployments
