

# ✅ Step 1 — Download the correct Go 1.22 version

Latest Go 1.22 release is **1.22.0** (or use 1.22.5 if you want a patched version).

Try this:

### ⭐ Install Go 1.22.0

```bash
wget https://go.dev/dl/go1.22.0.linux-amd64.tar.gz
```

Or latest patch version (recommended):

### ⭐ Install Go 1.22.5

```bash
wget https://go.dev/dl/go1.22.5.linux-amd64.tar.gz
```

---

# ✅ Step 2 — Extract it to /usr/local

For 1.22.0:

```bash
sudo tar -C /usr/local -xzf go1.22.0.linux-amd64.tar.gz
```

For 1.22.5:

```bash
sudo tar -C /usr/local -xzf go1.22.5.linux-amd64.tar.gz
```

---

# ✅ Step 3 — Add Go to PATH

```bash
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc
source ~/.bashrc
```

---

# ✅ Step 4 — Verify

```bash
go version
```

Expected:

```
go version go1.22.0 linux/amd64
```

or

```
go version go1.22.5 linux/amd64
```

Your system still doesn’t know about the **official Go binary** because the PATH is not updated correctly or you didn’t restart the shell.

Let’s fix it step by step.

---

# ✅ 1. Check if Go is installed in `/usr/local/go`

Run:

```bash
ls /usr/local/go/bin
```

You should see:

```
go  godoc  gofmt
```

If you see these files, Go is installed correctly — your PATH just isn’t pointing to it.

---

# ✅ 2. Add Go to PATH (correctly for Zsh on Fedora)

Since you are using **zsh**, you must update:

### ✔️ `~/.zshrc`

NOT `~/.bashrc`

Add the Go bin path:

```bash
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.zshrc
```

Then reload:

```bash
source ~/.zshrc
```

---

# ✅ 3. Verify PATH is correct

Run:

```bash
which go
```

Expected:

```
/usr/local/go/bin/go
```

Then:

```bash
go version
```

Expected:

```
go version go1.22.x linux/amd64
```

---

# ❗ If "which go" still shows nothing

Then reload ZSH completely:

```bash
exec zsh
```

Or log out and log in again.

---

# ❗ Fedora “go” suggestions (gcc-go / golang-bin) — ignore those

Fedora is suggesting:

```
'gcc-go'
'golang-bin'
```

But **do not install them**, since you are using the official Go (from go.dev).

---

# If the Go binary **does not exist** in `/usr/local/go`

Tell me what this prints:

```bash
ls -la /usr/local
```

Your Go binary **exists**, but your PATH does **not** include `/usr/local/go/bin`.
You're using **zsh**, and your PATH currently is:

```
/home/jihad/.nvm/...:/usr/local/bin:/usr/bin:...
```

`/usr/local/go/bin` is missing — so Go won’t run.

Let’s fix it properly.

---

# ✅ Step 1 — Add Go to zsh PATH

Run this:

```bash
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.zshrc
```

Then reload zsh:

```bash
source ~/.zshrc
```

---

# ✅ Step 2 — Check if PATH updated

```bash
echo $PATH
```

You should now see:

```
...:/usr/local/go/bin
```

---

# ✅ Step 3 — Verify Go

```bash
which go
go version
```

Expected:

```
/usr/local/go/bin/go
go version go1.22.x linux/amd64
```

---

# ❗ If STILL not working (rare)

Some Fedora setups use `~/.zprofile` or `/etc/zshenv`.

Try adding the same line to `~/.zprofile`:

```bash
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.zprofile
source ~/.zprofile
```

---

# ⚡ If you want a clean and guaranteed fix

Run this script (safe):

```bash
echo 'PATH=$PATH:/usr/local/go/bin' | sudo tee /etc/profile.d/go.sh >/dev/null
sudo chmod +x /etc/profile.d/go.sh
source /etc/profile.d/go.sh
```

This makes Go available system-wide.

---

If you run into any more errors, show me:

```bash
cat ~/.zshrc
```


