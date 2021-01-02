# Pterodactyl Wings Dependencies

## Info

[Back to Wings](/Pterodactyl/2%20-%20Wings)

<details>
<summary>Quick Install Dependencies</summary>
<p>

```sh
set -x ; sudo dnf install -y dnf-utils device-mapper-persistent-data lvm2 && sudo dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo && sudo dnf install -y https://download.docker.com/linux/centos/7/x86_64/stable/Packages/containerd.io-1.2.10-3.2.el7.x86_64.rpm && dnf install -y docker-ce --nobest && sudo systemctl enable --now docker && sudo dnf install -y mariadb mariadb-server && sudo systemctl enable --now mariadb && sudo firewall-cmd --add-port 8080/tcp --permanent && sudo firewall-cmd --add-port 2022/tcp --permanent && sudo firewall-cmd --add-port 3306/tcp --permanent && sudo firewall-cmd --permanent --zone=trusted --change-interface=pterodactyl0 && sudo firewall-cmd --zone=trusted --add-masquerade --permanent && sudo firewall-cmd --reload ; set +x ; echo 'done'
```

</p>
</details>
&nbsp;

<details>
<summary>Long Install Dependencies</summary>
<p>

### Docker

```sh
sudo dnf install -y dnf-utils device-mapper-persistent-data lvm2

sudo dnf config-manager --add-repo=https://download.docker.com/linux/centos/docker-ce.repo

sudo dnf install -y https://download.docker.com/linux/centos/7/x86_64/stable/Packages/containerd.io-1.2.10-3.2.el7.x86_64.rpm

dnf install -y docker-ce --nobest

sudo systemctl enable --now docker
```

### MariaDB

You only need to install MariaDB if the panel is not on the same machine

```sh
sudo dnf install -y mariadb mariadb-server

sudo systemctl enable --now mariadb
```

### FirewallD changes

```sh
sudo firewall-cmd --add-port 8080/tcp --permanent
sudo firewall-cmd --add-port 2022/tcp --permanent
sudo firewall-cmd --add-port 3306/tcp --permanent
sudo firewall-cmd --permanent --zone=trusted --change-interface=pterodactyl0
sudo firewall-cmd --zone=trusted --add-masquerade --permanent
sudo firewall-cmd --reload
```

</p>
</details>

## Info

[Next Step - Install](/Pterodactyl/2%20-%20Wings/2%20-%20Install.md)