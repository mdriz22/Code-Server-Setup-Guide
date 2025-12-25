# Code-Server-Setup-Guide

# For Install Code Server in Linux (Ubuntu):
curl -fsSL https://code-server.dev/install.sh | sh


# Manual initialization of Code Server (With && Without Password) :
code-server --bind-addr 127.0.0.1:8080

code-server --bind-addr 127.0.0.1:8080 --auth password 
**(Path for configure password : ~/.config/code-server/config.yaml )**

# Content in config.yaml :

bind-addr: 127.0.0.1:8080
auth: password
password: yourpasswordhere
cert: false


# Keep it running in the background
# If you close the terminal, both code-server and cloudflared stop. To run them in the background:

nohup code-server --bind-addr 127.0.0.1:8080 &


# Automatic restart service which system starts

# path:
sudo nano /etc/systemd/system/code-server.service

# content:

[Unit]
Description=Code Server
After=network.target

[Service]
Type=simple
User=hradmin
ExecStart=/usr/bin/code-server --bind-addr 127.0.0.1:8080 --auth password /home/hradmin/frappe-bench
Restart=always

[Install]
WantedBy=multi-user.target


# Reload, Enable and Start Service:

sudo systemctl daemon-reload
sudo systemctl enable code-server
sudo systemctl start code-server

# Check Status of service:

systemctl status code-server


