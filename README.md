Markdown


# 🌿 Paradise Nursery – React Deployment on Oracle Cloud

[![Deployment Status](https://img.shields.io/badge/Deployment-Live-success?style=for-the-badge&logo=oracle)](https://paradise-nursery.duckdns.org)
[![Security](https://img.shields.io/badge/SSL-Secured%20by%20Let's%20Encrypt-blue?style=for-the-badge&logo=letsencrypt)](https://paradise-nursery.duckdns.org)
[![Web Server](https://img.shields.io/badge/Nginx-Production%20Ready-green?style=for-the-badge&logo=nginx)](https://paradise-nursery.duckdns.org)

## 📌 Overview

**Paradise Nursery** is a React (Vite) application originally developed as an early learning project focused on frontend development. 

> ⚠️ **Note on UI/UX:** In this repository, the main emphasis is on **production deployment** rather than UI/UX refinement or responsiveness. The application contains UI mistakes made during development and is intentionally kept in its original state. It may not be fully responsive or optimized for mobile devices, as the primary objective of this project is to showcase real-world deployment and DevOps skills rather than frontend design quality.

The application is deployed on a production-grade Linux environment using **Oracle Cloud Infrastructure (OCI)** and demonstrates a full deployment workflow including server configuration, Nginx setup, domain management, and HTTPS security. It is served using Nginx, managed via SSH, exposed through DuckDNS, and secured using Let's Encrypt (Certbot).

---

## ⚙️ Tech Stack

| Component | Technology Used |
| :--- | :--- |
| **Frontend** | React (Vite) |
| **Cloud Provider** | Oracle Cloud Infrastructure (OCI) |
| **Operating System** | Oracle Linux 9 |
| **Web Server** | Nginx |
| **Domain & DNS** | DuckDNS (Free Dynamic DNS) |
| **Security** | Let's Encrypt (Certbot SSL) |
| **Tools & Version Control**| SSH, Git, GitHub, Linux CLI |

---

## 🏗️ Architecture

Cloud Infrastructure: Production deployment on Oracle Cloud VM.

Web Serving: Static hosting using Nginx with Single Page Application (SPA) routing support.

Remote Management: Secure remote deployment via SSH.

Networking: Free custom domain using DuckDNS.

Security: End-to-end HTTPS security using Let's Encrypt.

Operations: Linux server configuration, troubleshooting, and Git-based deployment workflow.

📦 Deployment Steps
1. Connect to VM via SSH
Bash


ssh -i ~/.ssh/<key> opc@<VM_PUBLIC_IP>
2. Clone Repository
Bash


git clone [https://github.com/Abed-ALMajeed-Kanso/paradise_nursery_deploy.git](https://github.com/Abed-ALMajeed-Kanso/paradise_nursery_deploy.git)
cd paradise_nursery_deploy
3. Install Dependencies & Build
Bash


npm install
npm run build
4. Prepare Web Directory
Bash


sudo mkdir -p /var/www/paradise_nursery
sudo cp -r dist/* /var/www/paradise_nursery/
5. Install & Start Nginx
Bash


sudo dnf install nginx -y
sudo systemctl enable nginx
sudo systemctl start nginx
6. Configure Nginx
Create the configuration file:

Bash


sudo nano /etc/nginx/conf.d/paradise_nursery.conf
Add the following block:

Nginx


server {
    listen 80;
    server_name paradise-nursery.duckdns.org;

    root /var/www/paradise_nursery;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }
}
7. Test & Restart Nginx
Bash


sudo nginx -t
sudo systemctl restart nginx
8. Configure DuckDNS
Point your domain via the DuckDNS dashboard:

Plaintext


paradise-nursery.duckdns.org → YOUR_VM_PUBLIC_IP
9. Install SSL (Certbot)
Install the Certbot Nginx package:

Bash


sudo dnf install certbot python3-certbot-nginx -y
Generate your SSL certificate:

Bash


sudo certbot --nginx -d paradise-nursery.duckdns.org
Test the automatic renewal process:

Bash


sudo certbot renew --dry-run
🔒 Final Result
App Live URL: https://paradise-nursery.duckdns.org

Security: Secure HTTPS connection established.

Server Environment: Production-ready Nginx server fully deployed on Oracle Cloud VM structure.
