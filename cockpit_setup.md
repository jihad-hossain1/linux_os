Here is the **clean, correct, updated method** to install and enable **Cockpit** on **Fedora 42 Workstation/Desktop**.

---

# ✅ **1. Install Cockpit**

Cockpit is included in Fedora’s official repositories.

```bash
sudo dnf install cockpit -y
```


# ✅ **2. Enable & Start Cockpit Service**

Cockpit uses a systemd socket, so enable it:

```bash
sudo systemctl enable --now cockpit.socket
```

Check status:

```bash
systemctl status cockpit.socket
```

Expected: **Active: active (running)**

---

# ✅ **3. Open Firewall Port (Optional for Desktop)**

Fedora Workstation usually allows Cockpit automatically.
If not, run:

```bash
sudo firewall-cmd --add-service=cockpit --permanent
sudo firewall-cmd --reload
```

Cockpit listens on **port 9090**.

---

# ✅ **4. Access Cockpit Web UI**

Open browser and go:

```
https://localhost:9090
```

or from another device:

```
https://<your-ip>:9090
```

Login with your **Fedora user account**.

---

# 🛑 **If you get "Connection failed"**

This is common. Check these:

### ✔ `cockpit.service` logs

```bash
sudo journalctl -u cockpit -f
```

### ✔ Check if socket is listening

```bash
sudo ss -tulpn | grep 9090
```

### ✔ Check SELinux (important)

Sometimes SELinux blocks cockpit modules.

```bash
sudo setenforce 0
```

If it works after disabling SELinux, then fix permanently with:

```bash
sudo sealert -a /var/log/audit/audit.log
```

---

# 🛠 **5. For Desktop: Make Cockpit Auto-start on Boot**

```bash
sudo systemctl enable cockpit
```

---

# 🎉 Done!

Cockpit should now work on Fedora 42 Desktop.

---

If you want, I can help you diagnose the error:

👉 **Send your output of:**

```
sudo systemctl status cockpit
sudo systemctl status cockpit.socket
sudo journalctl -u cockpit
```

## access on custom domain 

Run:

```bash
sudo nano /etc/cockpit/cockpit.conf
```

Delete everything and paste EXACTLY this:

```ini
[WebService]
Origins = https://main.team24u.xyz
ProtocolHeader = X-Forwarded-Proto
AllowUnencrypted = true
```

⚠ **Make sure `[WebService]` is the FIRST line.**
⚠ No trailing spaces, no extra characters, no quotes.

Save & exit.

---

# ✅ Restart Cockpit

```bash
sudo systemctl daemon-reload
sudo systemctl restart cockpit
```

Then check logs:

```bash
sudo journalctl -u cockpit -n 20
```

If the config is correct, **NO error** should appear.

---

# 🚀 After this, Cockpit will allow your domain:

```
https://main.team.xyz
```
