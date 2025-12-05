

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
