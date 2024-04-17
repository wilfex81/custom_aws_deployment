# Custom AWS Deployment Starter Pack

## Introduction
This starter pack provides a step-by-step guide for deploying a web application on AWS with custom configurations.

### Prerequisites
- Access to an AWS account
- Basic knowledge of Linux commands and AWS services

## Step 1: Initial Setup
1. Open necessary ports for SSH:
    ```bash
    sudo ufw allow OpenSSH
    ```

2. Enable the firewall:
    ```bash
    sudo ufw enable
    ```

3. Check firewall status:
    ```bash
    sudo ufw status
    ```

4. Install project dependencies including Gunicorn, curl, and Nginx.

## Step 2: Configuring Gunicorn and Nginx
1. Create Gunicorn socket file:
    ```bash
    sudo nano /etc/systemd/system/gunicorn.socket
    ```

2. Start and enable the Gunicorn socket:
    ```bash
    sudo systemctl start gunicorn.socket
    sudo systemctl enable gunicorn.socket
    ```

3. Check status of Gunicorn socket:
    ```bash
    sudo systemctl status gunicorn.socket
    ```

4. Check file creation for Gunicorn socket:
    ```bash
    file /run/gunicorn.sock
    ```

5. Check for errors in the Gunicorn socket:
    ```bash
    sudo journalctl -u gunicorn.socket
    ```

6. Reload systemd after making changes:
    ```bash
    sudo systemctl daemon-reload
    ```

7. Restart Gunicorn:
    ```bash
    sudo systemctl restart gunicorn
    ```

8. Check status of Gunicorn (Active and running):
    ```bash
    sudo systemctl status gunicorn
    ```

## Step 3: Testing Configuration
1. Test Gunicorn configuration:
    ```bash
    curl --unix-socket /run/gunicorn.sock localhost
    ```

## Step 4: Configuring Nginx
1. Configure Nginx proxy pass:
    ```bash
    sudo nano /etc/nginx/sites-available/(name)
    ```

2. Create symbolic link:
    ```bash
    sudo ln -s /etc/nginx/sites-available/(name) /etc/nginx/sites-enabled
    ```

3. Test Nginx configuration:
    ```bash
    sudo nginx -t
    ```

4. Restart Nginx:
    ```bash
    sudo systemctl restart nginx
    ```

## Step 5: Security and Optimization
1. Update firewall to delete allow rule for port:
    ```bash
    sudo ufw delete allow <port>
    ```

2. Allow Nginx full:
    ```bash
    sudo ufw allow 'Nginx Full'
    ```

## Step 6: Enhancements
- Add SSL/TLS configuration for Nginx.
- Implement monitoring using Prometheus, Grafana, or AWS CloudWatch.
- Automate deployment process with Ansible or Terraform.
- Implement backup strategy for server and application data.
- Plan for scalability using AWS Auto Scaling Groups.
- Keep configuration files under version control using Git.

## PS: Reference to Configuration Files
For actual data needed in the files mentioned above (e.g., `gunicorn.socket`, Nginx configuration file), please refer to the respective files created during the setup process(e,g., `gunicorn.socket.txt` for `gunicorn.soekct`)
