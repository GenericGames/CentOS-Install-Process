# Pterodactyl Setting up MySQL

## Info

[Back to README](README.md)

### Configuring MariaDB

```sh
mysql_secure_installation
```

```sql
## Change to your own secure password
Set root password? [Y/N] Y

## Get rid of users that could access the db by default
Remove anonymous users? [Y/N] Y

## Keep root off the external interfaces
Disallow root login remotely? [Y/N] Y

## Extra databases that aren't needed
Remove test database and access to it? [Y/N] Y

## Clears and sets all the changes made
Reload privilege tables now? [Y/N] Y
```

### Creating a database for Pterodactyl

Log In

```sh
mysql -u root -p
```

Set to use mysql

```sql
USE mysql;
## Note - If you have to exit at any point after this make sure to use this command again
```

Create user

```sql
## Remember to change 'somePassword' below to be a unique password specific to this account.
CREATE USER pterodactyl@127.0.0.1 IDENTIFIED BY 'somePassword';
```

Create database

```sql
CREATE DATABASE panel;
```

Assign permissions

```sql
GRANT ALL PRIVILEGES ON panel.* TO 'pterodactyl'@'127.0.0.1' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```

Leave MariaDB/MySQL

```sh
exit
```

### Creating a Database Host for Nodes

#### Dependencies

The dependencies only need to be installed if this system is not running the panel, otherwise they are already installed

```sh
sudo apt update
```

```sh
sudo apt install mariadb-server -y
```

#### Creating a user

```sh
mysql -u root -p
```

```sql
USE mysql;
```

Change IP below to server's IP that is running the panel & change username/password to unique user/pass

```sql
CREATE USER 'pterodactyluser'@'127.0.0.1' IDENTIFIED BY 'somepassword';
```

Assigning permissions

Change username and IP blow to whatever you used above

```sql
GRANT ALL PRIVILEGES ON *.* TO 'pterodactyluser'@'127.0.0.1' WITH GRANT OPTION;
```

```sql
FLUSH PRIVILEGES;
```

```sql
exit
```

Allowing external database access

```sh
cd /etc/mysql/
```

```sh
nano my.cnf
```

add below to file

```sh
[mysqld]
bind-address=0.0.0.0
```

```sh
systemctl restart mysql
```