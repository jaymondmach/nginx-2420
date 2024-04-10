# Tutorial For: Adding a Firewall and Reverse Proxy

## Introduction

Hello my name is Jaymond and in this tutorial I'll be introducing you to the setup of a firewall using UFW (Uncomplicated Firewall) and the configuration of a reverse proxy server to the backend. This setup enhances the security and accessibility of your backend service.

## Prerequisites

- A server with a backend binary ready to be deployed.
- Basic knowledge of Linux command line, systemd, Nginx, and UFW.

## Updates

### Firewall

1. **Install UFW**: UFW is a user-friendly front-end for managing iptables firewall rules. It is available in the standard repositories of most Linux distributions.

   ```bash
   sudo apt update
   sudo apt install ufw
   ```

2. **Enable UFW**: Enable the firewall and allow SSH connections to prevent locking yourself out.

   ```bash
   sudo ufw enable
   sudo ufw allow ssh
   ```

3. **Configure UFW Rules**: Allow traffic on ports 80 (HTTP) and 443 (HTTPS) for the reverse proxy, and on port 8080 for the backend service.

   ```bash
   sudo ufw allow 80
   sudo ufw allow 443
   sudo ufw allow 8080
   ```

### Backend

1. **Place Backend Binary**: Move the backend binary to a logical location, such as `/usr/local/bin`.

   ```bash
   sudo mv /path/to/your/backend /usr/local/bin/backend
   ```

2. **Create a New Service File**: Create a systemd service file to manage the backend as a service.

   ```bash
   sudo nano /etc/systemd/system/backend.service
   ```

   Add the following content to the file:

   ```ini
   [Unit]
   Description=Backend Service
   After=network.target

   [Service]
   ExecStart=/usr/local/bin/backend
   Restart=always
   User=yourusername
   Group=yourgroup

   [Install]
   WantedBy=multi-user.target
   ```

   Replace `yourusername` and `yourgroup` with your actual username and group.

3. **Start and Enable the Service**: Start the backend service and enable it to start on boot.

   ```bash
   sudo systemctl start backend
   sudo systemctl enable backend
   ```

4. **Edit Nginx Server Block**: Configure Nginx to act as a reverse proxy to the backend.

   ```bash
   sudo nano /etc/nginx/sites-available/default
   ```

   Add the following location block inside the `server` block:

   ```nginx
   location / {
       proxy_pass http://127.0.0.1:8080;
       proxy_set_header Host $host;
       proxy_set_header X-Real-IP $remote_addr;
       proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
       proxy_set_header X-Forwarded-Proto $scheme;
   }
   ```

   Test the Nginx configuration and reload the service:

   ```bash
   sudo nginx -t
   sudo systemctl reload nginx
   ```

## Testing

1. **Test the Backend**: Use `curl` or a tool like Postman to test the backend routes.

   ```bash
   curl http://146.190.12.184/hey
   curl -X POST -H "Content-Type: application/json" -d '{"message": "Hello from your server"}' http://146.190.12.184/echo
   ```

2. **Screenshots**: Include screenshots demonstrating the successful testing of your backend.

## Documents

- The `hello-server` file is included in the attachments directory of the notes.

## Conclusion

This tutorial has guided you through setting up a firewall using UFW and configuring a reverse proxy server for your backend. This setup enhances the security and accessibility of your backend service.
