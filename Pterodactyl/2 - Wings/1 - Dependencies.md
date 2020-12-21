# Pterodactyl Wings Dependencies

## Info

[Back to Wings](/Pterodactyl/2%20-%20Wings)

### Docker

```sh
dnf install -y dnf-utils device-mapper-persistent-data lvm2

dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo

sudo dnf install -y https://download.docker.com/linux/centos/7/x86_64/stable/Packages/containerd.io-1.2.10-3.2.el7.x86_64.rpm

dnf install -y docker-ce --nobest

systemctl enable docker
systemctl start docker
```

### MariaDB

You only need to install MariaDB if the panel is not on the same machine

```sh
dnf install -y mariadb mariadb-server

## Start maraidb
systemctl start mariadb
systemctl enable mariadb
```

### FirewallD changes

```sh
firewall-cmd --add-port 8080/tcp --permanent
firewall-cmd --add-port 2022/tcp --permanent
firewall-cmd --add-port 3306/tcp --permanent
firewall-cmd --permanent --zone=trusted --change-interface=pterodactyl0
firewall-cmd --zone=trusted --add-masquerade --permanent
firewall-cmd --reload
```

## Info

[Next Step - Install](/Pterodactyl/2%20-%20Wings/3%20-%20Install.md)