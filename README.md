# Code-Server-Setup-Guide

Quick guide to expose a local VS Code environment to the internet using Code Server.

---

# For Install Code Server in Linux (Ubuntu):
```bash
curl -fsSL https://code-server.dev/install.sh | sh
```


# Manual initialization of Code Server (With && Without Password) :
```bash
code-server --bind-addr 127.0.0.1:8080
```
```bash
code-server --bind-addr 127.0.0.1:8080 --auth password
```
**(Path for configure password : ~/.config/code-server/config.yaml )**

# Content in config.yaml :
```bash
bind-addr: 127.0.0.1:8080

auth: password

password: yourpasswordhere

cert: false
```

# Keep it running in the background
```bash
nohup code-server --bind-addr 127.0.0.1:8080 &
```

# Automatic restart service while system starts

# path:
```bash
sudo nano /etc/systemd/system/code-server.service
```
# Content in code-server.service :
```bash
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
```

# Reload, Enable and Start Service:
```bash
sudo systemctl daemon-reload
sudo systemctl enable code-server
sudo systemctl start code-server
```
# Check Status of service:
```bash
systemctl status code-server
```

