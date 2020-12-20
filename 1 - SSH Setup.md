# SSH Setup

## Info

[Back to README](README.md)

### Lock Root

```sh
sudo passwd --lock root
```

### Set up SSH, shortcut, key, disable password login

Update the system

```sh
sudo dnf update -y
```

Install openssh-server

```sh
sudo dnf install openssh-server
```

Verify that SSH service is running

```sh
sudo systemctl status sshd
```

If not running

```sh
sudo systemctl enable --now sshd
```

Configure firewall and open port 22

```sh
firewall-cmd --add-service ssh
```

To get IP

```sh
ip a
```

Test login with SSH

```sh
ssh user@"server-ip"
```

Create shortcut for ssh login on local machine

```sh
cd ~/.ssh
nano config

## add below to file

Host "hostname"
    User "username"
    Hostname "IP"
    Port "Port"
```

Test if shortcut works

```sh
ssh "hostname"
```

Set up login with key

```sh
ssh-copy-id "hostname" ## do this on local pc
```

Test if ssh-copy-id worked

```sh
ssh "hostname"
```

disable login with password

```sh
sudo nano /etc/ssh/sshd_config

## change from

"#PasswordAuthentication yes"

## to - Make sure to remove the # at the start

"PasswordAuthentication no"
```

restart ssh

```sh
systemctl restart sshd
```

test if password works

```sh
ssh -o PreferredAuthentications=password "hostname"
```
