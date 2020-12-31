# Pterodactyl Panel Install

## Info

[Back to Panel](/Pterodactyl/1%20-%20Panel)

<details>
<summary>Quick download/install</summary>
<p>

```sh
set -x ; sudo mkdir -p /var/www/pterodactyl && cd /var/www/pterodactyl && sudo curl -Lo panel.tar.gz https://github.com/pterodactyl/panel/releases/download/v1.1.1/panel.tar.gz && sudo tar -xzvf panel.tar.gz && sudo chmod -R 755 storage/* bootstrap/cache/ && sudo cp .env.example .env && sudo $(which composer) install --no-dev --optimize-autoloader && sudo php artisan key:generate --force ; set +x ; echo 'done'
```

</p>
</details>
&nbsp;

<details>
<summary>Long download/install</summary>
<p>

### Download Files

Make Dir and CD into it

```sh
sudo mkdir -p /var/www/pterodactyl
cd /var/www/pterodactyl
```

Download files

```sh
sudo curl -Lo panel.tar.gz https://github.com/pterodactyl/panel/releases/download/v1.1.1/panel.tar.gz
sudo tar -xzvf panel.tar.gz
sudo chmod -R 755 storage/* bootstrap/cache/
```

### Installation

Copy default default environment setting file, install core dependencies, and general all application encryption key

```sh
sudo cp .env.example .env
sudo $(which composer) install --no-dev --optimize-autoloader
```

Only run the command below if you are installing this Panel for the first time and do not have any Pterodactyl Panel data in the database

```sh
sudo php artisan key:generate --force
```

</p>
</details>

#### Environment Configuration

##### Setup

```sh
sudo php artisan p:environment:setup
```

<details>
<summary>Options</summary>
<p>
Note Everything in Brackets [] is default setting, press enter if you want default


```sh
Egg Author Email [unknown@unknown.com]
## For now use default (hit enter) when setting up on dedicated server type in your email

Application url [http://localhost]
## For now use default (hit enter) when setting up on dedicated server use https://simplegaming.gg/

Application timezone [America/New_York]:
## America/Phoenix

Cache Driver [Filesystem]:
## Redis

Session Driver [MySQL Database]:
## Redis

Queue Driver [MySQL Database]:
## Redis

Enable UI based settings editor (yes/no) [yes]:
## Default (hit enter)

Redis Host [localhost]:
## Default (hit enter)

Redis Password:
## Default (hit enter)

Redis Port [6379]:
## Default (hit enter)
```

</p>
</details>

##### Database

```sh
sudo php artisan p:environment:database
```

<details>
<summary>Options</summary>
<p>

Note Everything in Brackets [] is default setting, press enter if you want default


```sh
Database Host [127.0.0.1]:
## Default (hit enter)

Database Port [3306]:
Default (hit enter)

Database Name [panel]:
## default (hit enter) unless panel name was changed earlier in the configuration

Database Username [pterodactyl]:
## Default (hit enter) unless database username was changed earlier in the configuration

Database Password:
## Default is set to "somePassword" for testing purposes but should have been changed for actual install
```

</p>
</details>

##### Mail

```sh
sudo php artisan p:environment:mail
```

<details>
<summary>Options</summary>
<p>

Note Everything in Brackets [] is default setting, press enter if you want default


```sh
Which driver should be used for sending emails [SMTP Server]:
## Mail

Email address emails should originate from [no-reply@example.com]
## For now use default (hit enter)

Name that emails should appear from [Pterodactyl Panel]:
## Default (hit enter)

Encryption method to use [TLS]:
## None
```

</p>
</details>

#### Database Setup

```sh
sudo php artisan migrate --seed --force
```

##### Database User Setup

Add the first user

```sh
sudo php artisan p:user:make
```

<details>
<summary>Options</summary>
<p>

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

</p>
</details>

#### Set Permissions

```sh
sudo chown -R nginx:nginx *
```

### Queue Listeners

Crontab Configuration

```sh
sudo crontab -e
```

```sh
* * * * * php /var/www/pterodactyl/artisan schedule:run >> /dev/null 2>&1
```

```sh
cd /etc/systemd/system
sudo nano pteroq.service
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
User=nginx
Group=nginx
Restart=always
ExecStart=/usr/bin/php /var/www/pterodactyl/artisan queue:work --queue=high,standard,low --sleep=3 --tries=3

[Install]
WantedBy=multi-user.target
```

```sh
sudo systemctl enable --now redis
sudo systemctl enable --now pteroq.service
```

## Info

[Next Step - Webserver Configuration](/Pterodactyl/1%20-%20Panel/4%20-%20Webserver%20Configuration.md)