- Run this command on terminal

```bash
wget https://dev.mysql.com/get/Downloads/MySQL-8.4/mysql-8.4.0-1.el9.x86_64.rpm-bundle.tar
tar -xvf mysql-8.4.0-1.el9.x86_64.rpm-bundle.tar
sudo dnf install *.rpm

```

- Start & enable MySQL
```bash
sudo systemctl start mysqld
sudo systemctl enable mysqld
```

- Get temporary MySQL password
```bash
sudo grep 'temporary password' /var/log/mysqld.log
```
- You can skip this step - Secure MySQL
```bash
sudo mysql_secure_installation
```
 - Login with temporary password
```bash
sudo mysql -u root -p  #password found in temporary get password copy and past here
```

- Set a temporary strong password (Inside MySQL run this)

```bash
ALTER USER 'root'@'localhost' IDENTIFIED BY 'Temp@12345';
FLUSH PRIVILEGES;
```
- Remove password security policy
```bash
UNINSTALL COMPONENT 'file://component_validate_password';
```

- Change root password to ANYTHING you want
#### Now you can set your simple password, for example root:

```bash
ALTER USER 'root'@'localhost' IDENTIFIED BY 'root';
FLUSH PRIVILEGES;
```
### exit from terminal and login with set new password

- Create new user (login with new user)
```bash
CREATE USER 'admin'@'%' IDENTIFIED BY 'admin';
```

- Flush all privileges for this user
```bash
GRANT ALL PRIVILEGES ON *.* TO 'admin'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```

- allow remote access in MySQL
- Edit MySQL config:
```bash
sudo nano /etc/my.cnf
```

- Add:
```bash
bind-address = 0.0.0.0
```

- Restart MySQL:
```bash
sudo systemctl restart mysqld
```


---

## **Step 1 — Install Apache, PHP, and PHP extensions**

```bash
sudo dnf install httpd php php-mbstring php-mysqli php-json php-zip php-gd php-curl
```

Enable and start Apache:

```bash
sudo systemctl enable --now httpd
```

Check PHP version:

```bash
php -v
```

---

## **Step 2 — Install MySQL (if not installed)**

If you already have MySQL 8.4, skip this. Otherwise:

```bash
sudo dnf install https://dev.mysql.com/get/mysql-community-release-el9-1.noarch.rpm
sudo dnf config-manager --enable mysql-8.4-lts-community
sudo dnf install mysql-community-server
sudo systemctl enable --now mysqld
sudo grep 'temporary password' /var/log/mysqld.log
```

Run secure installation:

```bash
sudo mysql_secure_installation
```

---

## **Step 3 — Create MySQL admin user**

Login as root:

```bash
mysql -u root -p
```

Create user:

```sql
CREATE USER 'admin'@'localhost' IDENTIFIED BY 'admin';
GRANT ALL PRIVILEGES ON *.* TO 'admin'@'localhost' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```

---

## **Step 4 — Download phpMyAdmin**

```bash
cd /usr/share/
sudo wget https://www.phpmyadmin.net/downloads/phpMyAdmin-latest-all-languages.tar.gz
```
- Extract
```bash
sudo tar -xvf phpMyAdmin-latest-all-languages.tar.gz
sudo mv phpMyAdmin-*-all-languages phpmyadmin
sudo rm phpMyAdmin-latest-all-languages.tar.gz
```

---

## **Step 5 — Configure phpMyAdmin**

Copy the sample config:

```bash
cd /usr/share/phpmyadmin
sudo cp config.sample.inc.php config.inc.php
```

Edit config:

```bash
sudo nano config.inc.php
```

Paste the following (replace the blowfish secret):

```php
<?php
$i = 0;
$i++;
$cfg['Servers'][$i]['verbose'] = 'Local MySQL';
$cfg['Servers'][$i]['host'] = '127.0.0.1';
$cfg['Servers'][$i]['connect_type'] = 'tcp';
$cfg['Servers'][$i]['compress'] = false;
$cfg['Servers'][$i]['auth_type'] = 'cookie';
$cfg['Servers'][$i]['AllowNoPassword'] = false;
$cfg['blowfish_secret'] = 'YOUR_RANDOM_32_CHAR_STRING';
$cfg['DefaultLang'] = 'en';
$cfg['ServerDefault'] = 1;
$cfg['UploadDir'] = '';
$cfg['SaveDir'] = '';
```

Generate a random 32-character blowfish secret:

```bash
openssl rand -base64 32
```

Paste it into `$cfg['blowfish_secret']`.

---

## **Step 6 — Configure Apache**

Create Apache config:

```bash
sudo nano /etc/httpd/conf.d/phpmyadmin.conf
```

Paste:

```
Alias /phpmyadmin /usr/share/phpmyadmin

<Directory /usr/share/phpmyadmin/>
    AddDefaultCharset UTF-8
    <IfModule mod_authz_core.c>
        Require all granted
    </IfModule>
</Directory>
```

Restart Apache:

```bash
sudo systemctl restart php-fpm
sudo systemctl restart httpd

```

---

## **Step 7 — Fix SELinux for TCP connections**

```bash
sudo setsebool -P httpd_can_network_connect 1
sudo setsebool -P httpd_can_network_connect_db 1

```

This allows Apache / PHP-FPM to connect to MySQL over TCP.

---

## **Step 8 — Open phpMyAdmin**

Open in browser:

```
http://localhost/phpmyadmin
```

Login:

* **Username:** admin
* **Password:** admin







