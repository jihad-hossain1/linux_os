
If you want your Fedora laptop to **never sleep or suspend again**, you just need to **mask** those targets.
That will completely block any app, power event, or lid-close action from triggering sleep/suspend.

---

### 🛑 Disable Sleep and Suspend (permanently)

Run this command:

```bash
sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target
```

Then verify it worked:

```bash
systemctl status sleep.target suspend.target
```

You should now see:

```
Loaded: masked (Reason: Unit sleep.target is masked.)
```

That means **Fedora will never go to sleep** — even if you close the lid or hit the sleep shortcut.

---

### ⚙️ Optional: Prevent Lid-Close Sleep Too

Edit your logind config:

```bash
sudo nano /etc/systemd/logind.conf
```

Find or add these lines:

```
HandleLidSwitch=ignore
HandleLidSwitchDocked=ignore
HandleLidSwitchExternalPower=ignore
```

Then restart the service:

```bash
sudo systemctl restart systemd-logind
```

✅ Done!
Your Fedora 42 laptop will **stay awake 24/7** — no automatic sleep, suspend, or lid-triggered suspend.

