# Pterodactyl Upgrading Panel

## Info

[Back to Upgrading](/Pterodactyl/3%20-%20Upgrading)

### Maintenance Mode

```sh
cd /var/www/pterodactyl
sudo php artisan down
```

### Download Updated Files

[Check here for the most recent version command](https://pterodactyl.io/panel/1.0/upgrade/1.0.html#fetch-updated-files)

```sh
## Make sure to check the link above for the most recent version.
## Change "1.1.3" to the current version without the " marks
sudo curl -L https://github.com/pterodactyl/panel/releases/download/v"1.1.3"/panel.tar.gz | sudo tar -xzv
sudo chmod -R 755 storage/* bootstrap/cache
```

### Update Dependencies

```sh
sudo $(which composer) install --no-dev --optimize-autoloader
```

### Clear Compiled Template Cache

```sh
sudo php artisan view:clear
sudo php artisan config:clear
```

### Database Updates

```sh
sudo php artisan migrate --seed --force
```

### Set Permissions

```sh
sudo chown -R nginx:nginx *
```

### Restarting Queue Workers

```sh
sudo php artisan queue:restart
```

### Leave Maintenance Mode

Only leave maintenance mode if you are fully done upgrading and do not need to upgrade wings

```sh
cd /var/www/pterodactyl
sudo php artisan up
```

## Info

[Back to Upgrading](/Pterodactyl/3%20-%20Upgrading)