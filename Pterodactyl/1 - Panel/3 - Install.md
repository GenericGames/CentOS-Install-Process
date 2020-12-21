# Pterodactyl Panel Install

## Info

[Back to Panel](Pterodactyl/1%20-%20Panel)

### Download Files

Make Dir and CD into it

```sh
mkdir -p /var/www/pterodactyl
cd /var/www/pterodactyl
```

Download files

```sh
curl -Lo panel.tar.gz https://github.com/pterodactyl/panel/releases/download/v1.1.1/panel.tar.gz
tar -xzvf panel.tar.gz
chmod -R 755 storage/* bootstrap/cache/
```

### Installation

Copy default default environment setting file, install core dependencies, and general all application encryption key

```sh
cp .env.example .env
composer install --no-dev --optimize-autoloader
## The above command will tell you to not run it in root, ignore it.
## It will not work in this case if it's not ran in root.

## If the above command doesn't work try
sudo nano /root/.bashrc
## And add to the bottom
export PATH="$PATH:/usr/local/bin"
## If that doesn't work than do not in root
which composer
## Replace the path below with what the command above says
"/usr/local/bin/composer" install --no-dev --optimize-autoloader
```

Only run the command below if you are installing this Panel for the first time and do not have any Pterodactyl Panel data in the database

```sh
php artisan key:generate --force
```

#### Environment Configuration

##### Setup

```sh
php artisan p:environment:setup
## Note Everything in Brackets [] is default setting, press enter if you want default
```

```sh
Egg Author Email [unknown@unknown.com]
## For now use default (hit enter) when setting up on dedicated server type in your email
```

```sh
Application url [http://localhost]
## For now use default (hit enter) when setting up on dedicated server use https://simplegaming.gg/
```

```sh
Application timezone [America/New_York]:
## America/Phoenix
```

```sh
Cache Driver [Filesystem]:
## Redis
```

```sh
Session Driver [MySQL Database]:
## Redis
```

```sh
Queue Driver [MySQL Database]:
## Redis
```

```sh
Enable UI based settings editor (yes/no) [yes]:
## Default (hit enter)
```

```sh
Redis Host [localhost]:
## Default (hit enter)
```

```sh
Redis Password:
## Default (hit enter)
```

```sh
Redis Port [6379]:
## Default (hit enter)
```

##### Database

```sh
php artisan p:environment:database
## Note Everything in Brackets [] is default setting, press enter if you want default
```

```sh
Database Host [127.0.0.1]:
## Default (hit enter)
```

```sh
Database Port [3306]:
Default (hit enter)
```

```sh
Database Name [panel]:
## default (hit enter) unless panel name was changed earlier in the configuration
```

```sh
Database Username [pterodactyl]:
## Default (hit enter) unless database username was changed earlier in the configuration
```

```sh
Database Password:
## Default is set to "somePassword" for testing purposes but should have been changed for actual install
```

##### Mail

```sh
php artisan p:environment:mail
## Note Everything in Brackets [] is default setting, press enter if you want default
```

```sh
Which driver should be used for sending emails [SMTP Server]:
Mail
```

```sh
Email address emails should originate from [no-reply@example.com]
## For now use default (hit enter)
```

```sh
Name that emails should appear from [Pterodactyl Panel]:
## Default (hit enter)
```

```sh
Encryption method to use [TLS]:
None
```

#### Database Setup

```sh
php artisan migrate --seed --force
```

##### Database User Setup

Add the first user

```sh
php artisan p:user:make
```

```sh
Is this user an administrator (yes/no) [no]:
yes
```

```sh
Email Address:
## Put in email address
```

```sh
Username:
## Put in username
```

```sh
First Name:
## Put in first name
```

```sh
Last Name:
## put in last name
```

```sh
Password:
## For testing we will use "Password1" when dedicated is set up we will use actual password. Enter password - Note: Must be at a minimum 8 characters, contain one capital, and one number
```

#### Set Permissions

```sh
chown -R nginx:nginx *
```

### Queue Listeners

Crontab Configuration

```sh
sudo crontab -e
```

```sh
## Note: The above command opens in vim.
## To save and exit press esc and type ":ZZ" and to just exit use "ZQ" than press enter
* * * * * php /var/www/pterodactyl/artisan schedule:run >> /dev/null 2>&1
```

```sh
cd /etc/systemd/system
nano pteroq.service
```

```conf
# Pterodactyl Queue Worker File
# ----------------------------------

[Unit]
Description=Pterodactyl Queue Worker
After=redis.service

[Service]
# On some systems the user and group might be different.
# Some systems use `apache` or `nginx` as the user and group.
User=www-data
Group=www-data
Restart=always
ExecStart=/usr/bin/php /var/www/pterodactyl/artisan queue:work --queue=high,standard,low --sleep=3 --tries=3

[Install]
WantedBy=multi-user.target
```

```sh
systemctl enable --now redis
sudo systemctl enable --now pteroq.service
```

## Info

[Next Step - Webserver Configuration](Pterodactyl/1%20-%20Panel/4%20-%20Webserver%20Configuration.md)