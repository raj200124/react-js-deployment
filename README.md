# Deploying a ReactJS Application on an EC2 Instance with Nginx

This guide will walk you through the process of deploying a ReactJS application on an Amazon EC2 instance using Nginx as the web server. By following these steps, you will be able to serve your ReactJS application to the web, making it accessible to users.

## Prerequisites

Before you begin, make sure you have the following:

- An AWS account with EC2 access
- An EC2 instance running a Linux-based operating system (e.g., Amazon Linux, Ubuntu)
- Node.js and npm installed on your EC2 instance
- A ReactJS application ready for deployment

## Step 1: Connect to Your EC2 Instance

Use SSH to connect to your EC2 instance. Replace `your-ec2-ip` with the public IP address or DNS name of your EC2 instance.

```bash
ssh -i your-ec2-key.pem ec2-user@your-ec2-ip
```

## Step 2: Update the System

Update the package list and install any available updates:

```bash
sudo yum update -y
```

## Step 3: Install Nginx

Install Nginx on your EC2 instance:

```bash
sudo yum install nginx -y
```

## Step 4: Start and Enable Nginx

Start the Nginx service and enable it to start on boot:

```bash
sudo systemctl start nginx
sudo systemctl enable nginx
```

## Step 5: Configure Nginx for Your React Application

Create a new Nginx server block configuration file for your React application. Replace `your-domain.com` with your domain name or IP address:

```bash
sudo nano /etc/nginx/conf.d/your-domain.conf
```

Add the following configuration to the file, adjusting the paths as needed for your specific setup:

```nginx
server {
    listen 80;
    server_name your-domain.com www.your-domain.com;

    root /var/www/html;
    index index.html;

    location / {
        try_files $uri /index.html;
    }
}
```

Save and exit the file (`Ctrl+O`, then `Enter`, followed by `Ctrl+X`).

## Step 6: Deploy Your React Application

Copy your ReactJS application build files to the web server's root directory:

```bash
sudo rm -rf /var/www/html/*
sudo cp -r /path/to/your/react-app/build/* /var/www/html/
```

## Step 7: Test the Nginx Configuration

Check the Nginx configuration for any syntax errors:

```bash
sudo nginx -t
```

If there are no errors, you should see the following message: "syntax is okay" and "test is successful."

## Step 8: Restart Nginx

Reload Nginx to apply the new configuration:

```bash
sudo systemctl restart nginx
```

## Step 9: Configure Your Domain

If you're using a domain name, configure your domain registrar to point to your EC2 instance's public IP address.

## Step 10: Access Your React Application

Visit your domain or your EC2 instance's public IP address in a web browser to access your deployed ReactJS application.

Congratulations! Your ReactJS application is now successfully deployed on an EC2 instance using Nginx as the web server.
