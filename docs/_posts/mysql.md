---
title: Mysql Related
---

Mysql server setup
======

<br>

Installing mysql server and client
-----

```
sudo apt-get update
sudo apt-get install mysql-server
sudo apt-get install mysql-client
```

<br>

Testing if mysql is successfully installed
------

```
sudo netstat -tap | grep mysql
```

<br>

Restarting mysql server
------

```
sudo service mysql restart
```

<br>

User and authentication setup
------

```
# logging in as root
sudo mysql -uroot -proot

# creating a new user
CREATE USER lduan;

# changing authentication information
UPDATE mysql.user SET authentication_string=123456 WHERE user='lduan';

UPDATE mysql.user SET host='localhost' WHERE user = 'lduan';

# Granting user privileges to access "*.*" (all tables in all databases)
GRANT ALL PRIVILEGES on *.* to 'lduan'@'localhost';
FLUSH PRIVILEGES;
```

<br>

Setting remote access for Mysql server
------

<br>

### Edit the config file
```
sudo vim /etc/mysql/mysql.conf.d/mysqld.cnf
```

### Comment out the line:
```
bind-address = 127.0.0.1htop
```

### Save and exit

### Inside Mysql client console
```
GRANT ALL PRIVILEGES ON *.* to lduan@"%" identified by "123456" WITH GRANT OPTION;
FLUSH PRIVILEGES;
QUIT
```

<br>

Setting up rules for firewall to allow mysql port to be connected
------

```
sudo ufw allow 3306
```

<br>

Restart service once more
------

<br>

Import .sql file using command line
======

<br>

Create a database
------

```
CREATE DATABASE <database name>;
```

<br>

Import from .sql file without showing progress
------

```
mysql -p -u lduan <database name> < filename.sql
```

<br>

Import from .sql file showing progress
------

```
# If pv is not installed, install it first
sudo apt-get install pv
# Then run the following command
pv sqlfile.sql | mysql -uxxx -pxxxx dbname
```
