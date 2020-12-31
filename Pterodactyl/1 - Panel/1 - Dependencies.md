# Pterodactyl Panel Dependencies

## Info

[Back to Panel](/Pterodactyl/1%20-%20Panel)

This is only done on one machine.
If the panel is already installed move onto [Pterodactyl Wings install](3%20-%20Pterodactyl%20Wings%20install.md).

[Link to documentation](https://pterodactyl.io/community/installation-guides/panel/centos8.html#installing-the-panel)

### Install Dependencies

<details>
<summary>Quick Install Dependencies</summary>
<p>

```sh
set -x ; sudo dnf install -y policycoreutils selinux-policy selinux-policy-targeted setroubleshoot-server setools setools-console mcstrans && sudo dnf install -y mariadb mariadb-server && sudo systemctl enable --now mariadb && sudo dnf install -y epel-release && sudo dnf install -y https://rpms.remirepo.net/enterprise/remi-release-8.rpm && sudo dnf module enable -y php:remi-7.4 && sudo dnf update -y && sudo dnf install -y php php-{common,fpm,cli,json,mysqlnd,gd,mbstring,pdo,zip,bcmath,dom,opcache} && sudo dnf install php-cli php-json php-zip wget unzip && curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer && sudo dnf install -y nginx && sudo firewall-cmd --add-service=http --permanent && sudo firewall-cmd --add-service=https --permanent && sudo firewall-cmd --reload && sudo systemctl enable --now nginx && sudo dnf install -y redis && sudo systemctl enable --now redis && sudo setsebool -P httpd_can_network_connect 1 && sudo setsebool -P httpd_execmem 1 && sudo setsebool -P httpd_unified 1 ; set +x ; echo 'done'
```

</p>
</details>
&nbsp;

<details>
<summary>Long Install Dependencies</summary>
<p>

SELinux tools

```sh
sudo dnf install -y policycoreutils selinux-policy selinux-policy-targeted setroubleshoot-server setools setools-console mcstrans
```

MariaDB

```sh
sudo dnf install -y mariadb mariadb-server

## Enable & start maraidb
sudo systemctl enable --now mariadb
```

PHP 7.4

```sh
## Install Repos
sudo dnf install -y epel-release
sudo dnf install -y https://rpms.remirepo.net/enterprise/remi-release-8.rpm
sudo dnf module enable -y php:remi-7.4

## Get dnf updates
sudo dnf update -y

## Install PHP 7.4
sudo dnf install -y php php-{common,fpm,cli,json,mysqlnd,gd,mbstring,pdo,zip,bcmath,dom,opcache}
```

Composer

```sh
sudo dnf install php-cli php-json php-zip wget unzip
curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer
```

Nginx

```sh
sudo dnf install -y nginx

sudo firewall-cmd --add-service=http --permanent
sudo firewall-cmd --add-service=https --permanent
sudo firewall-cmd --reload

sudo systemctl enable --now nginx
```

Redis

```sh
sudo dnf install -y redis

sudo systemctl enable --now redis
```

SELinux commands
The following command will allow nginx to work with redis

```sh
sudo setsebool -P httpd_can_network_connect 1
sudo setsebool -P httpd_execmem 1
sudo setsebool -P httpd_unified 1
```
</p>
</details>

## Info

[Next Step - Setting up MySQL](/Pterodactyl/1%20-%20Panel/2%20-%20Setting%20up%20MySQL.md)