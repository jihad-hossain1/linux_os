On Linux (Fedora 42), the **copy line up/down** shortcuts often do **not work** because GNOME/Fedora blocks those keys.

In VS Code (Windows):

* **Shift + Alt + Up** → Copy line up
* **Shift + Alt + Down** → Copy line down

On Fedora GNOME, these keys are **taken by system window movement**.

---

# ✅ FIX — Disable GNOME Conflicting Shortcuts

Fedora GNOME uses these shortcuts for moving windows between monitors or workspaces.

Run this in terminal:

### **Disable system shortcuts that conflict**

```bash
gsettings set org.gnome.desktop.wm.keybindings move-to-workspace-up "[]"
gsettings set org.gnome.desktop.wm.keybindings move-to-workspace-down "[]"
gsettings set org.gnome.desktop.wm.keybindings move-to-workspace-left "[]"
gsettings set org.gnome.desktop.wm.keybindings move-to-workspace-right "[]"
```

Then restart GNOME or logout/login.

---

# ✅ FIX — Rebind VS Code Manually (If needed)

1. Open **VS Code**
2. Press: **Ctrl + K, Ctrl + S**
3. Search: `copy line up`
4. Set to:

   * Copy line up → **Shift + Alt + Up**
   * Copy line down → **Shift + Alt + Down**

If GNOME still blocks it, set alternative Windows-style shortcuts:

### Option B: Use Ctrl+Alt

```text
Ctrl + Alt + Up   = Copy line up
Ctrl + Alt + Down = Copy line down
```

These rarely conflict on Fedora.

---

# 🔍 Want True Windows Behavior?

Install the **Windows Keymap** extension:

```
Ctrl + Shift + X → search: "Windows Keymap"
```

This restores Windows shortcuts including line-copy—but you still must disable GNOME conflicts as above.

---

# ✅ Summary

| Problem                      | Reason                 | Fix                               |
| ---------------------------- | ---------------------- | --------------------------------- |
| Shift + Alt + Up not working | Fedora/GNOME blocks it | Disable GNOME workspace shortcuts |
| VS Code not copying line     | Wrong keymap           | Rebind manually                   |
| Want full Windows behavior   | Linux defaults differ  | Install Windows Keymap extension  |

---

If you want, tell me your **Linux desktop environment (GNOME/KDE/i3)** and I’ll give the exact shortcut fix for your setup.
