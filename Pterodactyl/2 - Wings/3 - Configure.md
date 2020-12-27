# Pterodactyl Wings Configure

## Info

[Back to Wings](/Pterodactyl/2%20-%20Wings)

### Set up Node

Go into admin control on the panel, select **Locations** under **MANAGEMENT** and create a location
After creating a location go to **Nodes** and create a new node

```sh
cd /etc/pterodactyl
nano config.yml
```

Select the node you just created and click on **Configuration** and copy the text and paste it in **Config.yml**

### Start Wings

```sh
wings --debug
## If the above command says that wings is not installed run the below command
/usr/local/bin/wings --debug
```

### Daemonizing

```sh
cd /etc/systemd/system
nano wings.service
```

Paste the text below into wings.service

```conf
[Unit]
Description=Pterodactyl Wings Daemon
After=docker.service

[Service]
User=root
WorkingDirectory=/etc/pterodactyl
LimitNOFILE=4096
PIDFile=/var/run/wings/daemon.pid
ExecStart=/usr/local/bin/wings
Restart=on-failure
StartLimitInterval=600

[Install]
WantedBy=multi-user.target
```

### Start & Enable wings

```sh
systemctl enable --now wings
```

## Info

[Next Step - Setting up MySQL](/Pterodactyl/2%20-%20Wings/4%20-%20Setting%20up%20MySQL.md)
