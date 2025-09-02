# MySQL Network Setup Guide for macOS

To use MySQL over a network on a macOS system, you must install the MySQL Server software and configure it to allow remote connections, typically by changing the bind-address in the configuration file to allow connections from external IP addresses rather than just localhost. Additionally, you may need to configure the firewall to permit connections to the MySQL port (default 3306) and grant the necessary permissions to remote users within MySQL itself.

## 1. Install MySQL Server on macOS

* Download the macOS native package installer (.dmg file) from the official MySQL website
* Double-click the downloaded file to mount the DMG and then open the .pkg file within to launch the installation wizard
* Follow the steps in the installer to install MySQL Community Server and set a root password

## 2. Configure MySQL for Remote Connections

### Locate the MySQL configuration file:
If you installed MySQL via Homebrew, you can find the configuration file using:
```bash
cd /opt/homebrew
find . -name my.cnf
```

This typically returns two locations:
* `/opt/homebrew/etc/my.cnf` (main config file)
* `/opt/homebrew/Cellar/mysql/8.0.33_3/.bottle/etc/my.cnf` (version-specific config)

### Modify the bind-address:
* Edit the configuration file (typically the one in `/opt/homebrew/etc/my.cnf`)
* Find the `bind-address` line in the `[mysqld]` section. By default, it's often set to `127.0.0.1` (localhost)
* Change `bind-address` to `0.0.0.0` in the `[mysqld]` section:
```ini
[mysqld]
bind-address = 0.0.0.0
```
  This allows connections from any IP address

### Restart the MySQL service:
After saving the changes, restart the MySQL service:
```bash
sudo systemctl restart mysql
```

## 3. Configure the Firewall

Ensure that your macOS firewall is configured to allow incoming connections to the MySQL port, which is 3306 by default.

## 4. Grant Remote Access in MySQL

Log in to MySQL as root or a user with administrative privileges, then create a remote user and grant permissions:

### Create a remote user:
```sql
CREATE USER 'remote'@'%' IDENTIFIED BY 'dummy-pw';
```
* The `'remote'@'%'` format means user 'remote' can connect from any host (`%` is a wildcard)

* Replace the dummy password with your own secure password

### Grant privileges:
```sql
GRANT ALL PRIVILEGES ON *.* TO 'remote'@'%' WITH GRANT OPTION;
```
* `ALL PRIVILEGES` grants full access to all databases and tables (`*.*`)

* `WITH GRANT OPTION` allows this user to grant privileges to other users

### Apply the changes:
```sql
FLUSH PRIVILEGES;
```

### Verify the user was created:
```sql
SELECT user FROM mysql.user;
```
This will show all users in the MySQL system, including your new 'remote' user.
