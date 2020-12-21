# Setting up MySQL

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

### Creating a database for Pterodactyl Panel

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
