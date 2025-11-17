

# ✅ Step-1: Install cloudflared (if not installed)

```bash
sudo dnf install cloudflared   # Fedora
```

Or if installed manually, skip.

# ✅ cloudflared tunnel login

```bash
cloudflared tunnel login
```
- confirm your login credential are ok.
- check this command
```bash
ls /home/<your user name>/.cloudflared # here you have find cert.pem file this are your credential
```

# ✅ Create a file on /home/<your user name>/.cloudflared this folder 'that's mean home folder'
```bash
sudo touch config.yml
# open this file on text editor or sudo nano config.yml
```
- file content have like this
```bash
tunnel: team24
credentials-file: /home/jihad/.cloudflared/13123-4fe6-47a1-beed-34123.json

ingress:
  - hostname: yourdomain.com
    service: http://localhost:7000
    
  - hostname: main.yourdomain.com
    service: http://localhost:9090
    
  - service: http_status:404
```


# ✅ Create folder and file

```bash
# open terminal and command
cd /
cd /etc
sudo mkdir cloudflared
sudo touch cert.pem config.yml <your tunnel json file name>.json
```
- now open this file one by one and modify this files
```bash
sudo nano confg.yml
# copy file source from here file name config.yml /home/<your user name>/.cloudflared as like /home/jihad/.cloudflared
# cntrl + o , enter , cntrl + x
```

```bash
sudo nano cert.pem
# copy file source from here cert.pem /home/<your user name>/.cloudflared as like /home/jihad/.cloudflared
# cntrl + o , enter , cntrl + x
```

```bash
sudo nano tunnel_json_file_name.json
# copy file source from here tunnel_json_file_name.json /home/<your user name>/.cloudflared as like /home/jihad/.cloudflared
# cntrl + o , enter , cntrl + x
```


---

# ✅ Create a systemd service file

Create the file:

```bash
sudo nano /etc/systemd/system/cloudflared.service
```

Paste this:

```
[Unit]
Description=Cloudflare Tunnel
After=network-online.target
Wants=network-online.target

[Service]
Type=simple
User=root
ExecStart=/usr/bin/cloudflared tunnel run <YOUR_TUNNEL_NAME>
WorkingDirectory=/etc/cloudflared
Restart=always
RestartSec=5s

[Install]
WantedBy=multi-user.target
```

---

# ✅ Step-3: Reload systemd

```
sudo systemctl daemon-reload
```

---

# ✅ Step-4: Enable cloudflared on boot

```
sudo systemctl enable cloudflared
```

---

# ✅ Step-5: Start the service now

```
sudo systemctl start cloudflared
```

---

# 🔍 Check service status

```
sudo systemctl status cloudflared
```

---

# ⚠️ If you use named tunnels

If your tunnel has a name (recommended):

Find your tunnel name:

```
cloudflared tunnel list
```

Then create service file with the tunnel name:

```
ExecStart=/usr/bin/cloudflared tunnel run <YOUR_TUNNEL_NAME>
```

Example:

```
ExecStart=/usr/bin/cloudflared tunnel run mytunnel
```

---

# 🎉 Now cloudflared auto-starts on every boot.

If you want, I can also give:
✅ Systemd service for ingress rules
✅ Log file setup
✅ Restart on failure configuration
Just tell me!
