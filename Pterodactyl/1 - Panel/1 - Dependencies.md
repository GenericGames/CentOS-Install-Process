# Pterodactyl Panel Dependencies

## Info

[Back to Panel](/Pterodactyl/1%20-%20Panel)

This is only done on one machine.
If the panel is already installed move onto [Pterodactyl Wings install](3%20-%20Pterodactyl%20Wings%20install.md).

[Link to documentation](https://pterodactyl.io/community/installation-guides/panel/centos8.html#installing-the-panel)

### Before Entering Root

```sh
# Run this whole command as one
sudo tee /etc/profile.d/nano.sh <<EOF
export VISUAL="nano"
export EDITOR="nano"
EOF
```

```sh
sudo nano /root/.bashrc
```

Add the lines below to the bottom of the file

```conf
export PATH="$PATH:/usr/local/bin"
export EDITOR=nano
```

### Install Dependencies

Switch to root. You will need to be in root for multiple of the below commands

```sh
sudo -s
```

<details>
<summary>Quick Install Dependencies</summary>
<p>

```sh
set -x ; dnf install -y policycoreutils selinux-policy selinux-policy-targeted setroubleshoot-server setools setools-console mcstrans && dnf install -y mariadb mariadb-server && systemctl enable --now mariadb && dnf install -y epel-release && dnf install -y https://rpms.remirepo.net/enterprise/remi-release-8.rpm && dnf module enable -y php:remi-7.4 && dnf update -y && dnf install -y php php-{common,fpm,cli,json,mysqlnd,gd,mbstring,pdo,zip,bcmath,dom,opcache} && dnf install php-cli php-json php-zip wget unzip && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && dnf install -y nginx && firewall-cmd --add-service=http --permanent && firewall-cmd --add-service=https --permanent && firewall-cmd --reload && systemctl enable --now nginx && dnf install -y redis && systemctl enable --now redis && setsebool -P httpd_can_network_connect 1 && setsebool -P httpd_execmem 1 && setsebool -P httpd_unified 1 ; set +x ; echo 'done'
```

</p>
</details>
&nbsp;

SELinux tools

```sh
dnf install -y policycoreutils selinux-policy selinux-policy-targeted setroubleshoot-server setools setools-console mcstrans
```

MariaDB

```sh
dnf install -y mariadb mariadb-server

## Enable & start maraidb
systemctl enable --now mariadb
```

PHP 7.4

```sh
## Install Repos
dnf install -y epel-release
dnf install -y https://rpms.remirepo.net/enterprise/remi-release-8.rpm
dnf module enable -y php:remi-7.4

## Get dnf updates
dnf update -y

## Install PHP 7.4
dnf install -y php php-{common,fpm,cli,json,mysqlnd,gd,mbstring,pdo,zip,bcmath,dom,opcache}
```

Composer

```sh
dnf install php-cli php-json php-zip wget unzip
curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
```

Nginx

```sh
dnf install -y nginx

firewall-cmd --add-service=http --permanent
firewall-cmd --add-service=https --permanent
firewall-cmd --reload

systemctl enable --now nginx
```

Redis

```sh
dnf install -y redis

systemctl enable --now redis
```

SELinux commands
The following command will allow nginx to work with redis

```sh
setsebool -P httpd_can_network_connect 1
setsebool -P httpd_execmem 1
setsebool -P httpd_unified 1
```
## Info

[Next Step - Setting up MySQL](/Pterodactyl/1%20-%20Panel/2%20-%20Setting%20up%20MySQL.md)