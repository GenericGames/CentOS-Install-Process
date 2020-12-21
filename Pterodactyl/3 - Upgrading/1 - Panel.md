# Pterodactyl Upgrading Panel

## Info

[Back to Upgrading](/Pterodactyl/3%20-%20Upgrading)

### Maintenance Mode

```sh
cd /var/www/pterodactyl
php artisan down
```

### Download Updated Files

```sh
cd /var/www/pterodactyl
curl -L https://github.com/pterodactyl/panel/releases/download/v1.1.3/panel.tar.gz | tar -xzv
chmod -R 755 storage/* bootstrap/cache
```

### Update Dependencies

```sh
composer install --no-dev --optimize-autoloader
## If the above command doesn't work try
sudo nano /root/.bashrc
## And add to the bottom
export PATH="$PATH:/usr/local/bin"
## If that doesn't work than do not in root
which composer
## Replace the path below with what the command above says
/usr/local/bin/composer install --no-dev --optimize-autoloader
```

### Clear Compiled Template Cache

```sh
php artisan view:clear
php artisan config:clear
```

### Database Updates

```sh
php artisan migrate --seed --force
```

### Set Permissions

```sh
chown -R nginx:nginx *
```

### Restarting Queue Workers

```sh
php artisan queue:restart
```

### Leave Maintenance Mode

Only leave maintenance mode if you are fully done upgrading and do not need to upgrade wings

```sh
cd /var/www/pterodactyl
php artisan up
```

## Info

[Back to Upgrading](/Pterodactyl/3%20-%20Upgrading)