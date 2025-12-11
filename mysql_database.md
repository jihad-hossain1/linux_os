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






