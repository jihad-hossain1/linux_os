 ✅ — you want Fedora to **use Ethernet (enp2s0)** as the **first priority**, and **Wi-Fi (wlp1s0)** only if Ethernet is disconnected.

Here’s how to do it properly:

---

### 🧭 Option 1: Using NetworkManager (Recommended)

Fedora uses **NetworkManager**, so you can easily control connection priorities.

#### Step 1 — Check your connections:

```bash
nmcli connection show
```

You’ll see something like:

```
NAME                UUID                                  TYPE      DEVICE
Wired connection 1  abcd-efgh-1234-5678                  ethernet  enp2s0
MyWiFi              zyxw-vuts-9876-5432                  wifi      wlp1s0
```

#### Step 2 — Set Ethernet to higher priority (lower `connection.autoconnect-priority`)

Run these two commands:

```bash
sudo nmcli connection modify "Wired connection 1" connection.autoconnect-priority 10
sudo nmcli connection modify "MyWiFi" connection.autoconnect-priority 0
```

> Higher number = higher priority.

So here, **Ethernet = 10** and **Wi-Fi = 0**, meaning Fedora will always prefer Ethernet when both are available.

#### Step 3 — Restart NetworkManager

```bash
sudo systemctl restart NetworkManager
```

Or simply reconnect:

```bash
nmcli connection down "MyWiFi" && nmcli connection up "Wired connection 1"
```

---

### 🧰 Option 2: Command-line only (no GUI)

If you just want a one-liner approach:

```bash
sudo nmcli connection modify "enp2s0" connection.autoconnect-priority 10
sudo nmcli connection modify "wlp1s0" connection.autoconnect-priority 0
```

---

### ✅ Verify it’s working

You can check the routing table to confirm Ethernet is preferred:

```bash
ip route
```

You should see the **default route (`default via ...`)** going through your Ethernet device (`enp2s0`) when it’s plugged in.

If you unplug the cable, NetworkManager will automatically switch to Wi-Fi.

---

