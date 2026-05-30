# Static Site Server Configuration & Deployment

This project documents the installation and configuration of an Nginx web server on a remote Linux instance (Debian 12 on Google Cloud Platform) to serve a static website, alongside an automated deployment pipeline utilizing `rsync`.

## Project Deliverables
- [x] Provision a remote Linux instance with functional SSH access.
- [x] Install and configure Nginx to serve assets from a dedicated web root.
- [x] Develop a local static website structure containing HTML and CSS.
- [x] Configure a localized automated deployment script using `rsync`.
- [x] Bind configuration to the server's public IP address.

---

## Technical Implementation

### 1. Web Server Installation & Directory Setup
After connecting to the server via SSH, the package manager was updated and Nginx was installed:

```bash
sudo apt update
sudo apt install nginx -y
```

A dedicated directory structure was created under the standard /var/www/ pathway, and directory permissions were modified to allow management without permanent root escalation:
```bash
sudo mkdir -p /var/www/my-static-site
sudo chown -R $USER:$USER /var/www/my-static-site
```

### 2. Nginx Server Block Configuration

A new configuration profile was isolated within sites-available to map incoming HTTP traffic on port 80 to the web root:

File path: /etc/nginx/sites-available/my-static-site


The site configuration was activated via a symbolic link, validated for syntax errors, and loaded into the active runtime:
```bash
sudo ln -s /etc/nginx/sites-available/my-static-site /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl restart nginx
```

## Project Url
https://roadmap.sh/projects/static-site-server
