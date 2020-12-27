# Setting up MySQL

## Info

[Back to Wings](/Pterodactyl/2%20-%20Wings)

### Configuring MariaDB

This only needs to be done if this server does not run the panel as well

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

### Creating a database for Pterodactyl Nodes

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
FLUSH PRIVILEGES;
exit
```

Allowing external database access

```sh
cd /etc/
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

### Adding database to panel

On the Admin Control select **Databases** and select **Create New** fill in the info used to create the database & user

## Info

[Back to Pterodactyl](/Pterodactyl)