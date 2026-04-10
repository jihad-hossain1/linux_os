
### Add cloudflare-warp.repo to /etc/yum.repos.d/
```bash
curl -fsSl https://pkg.cloudflareclient.com/cloudflare-warp-ascii.repo | sudo tee /etc/yum.repos.d/cloudflare-warp.repo
```

- then run this 
```bash 
sudo yum install cloudflare-warp 
```

```bash 
warp-cli registration new
```

```bash 
warp-cli connect
```

- run this and confirm on show warp run or active this status 'warp=on'
```bash 
curl https://www.cloudflare.com/cdn-cgi/trace
```

### read manual doc [Here](https://pkg.cloudflareclient.com/) 
