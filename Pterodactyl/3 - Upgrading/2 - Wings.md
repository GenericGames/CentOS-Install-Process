# Pterodactyl Upgrading Wings

## Info

[Back to Upgrading](/Pterodactyl/3%20-%20Upgrading)

### Maintenance Mode

Make sure the system running the panel is in maintenance mode

```sh
cd /var/www/pterodactyl
php artisan down
```

### Download Updated Binary

```sh
cd /usr/local/bin
curl -L -o /usr/local/bin/wings https://github.com/pterodactyl/wings/releases/download/v1.1.3/wings_linux_amd64
chmod u+x /usr/local/bin/wings
```

### Restart Process

```sh
systemctl restart wings
```

### Leave Maintenance Mode & Restart Queue Workers

Leave Maintenance Mode & Restart Queue Workers on the system running the panel

```sh
cd /var/www/pterodactyl
php artisan up
php artisan queue:restart
```

## Info

[Back to Upgrading](/Pterodactyl/3%20-%20Upgrading)