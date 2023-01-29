# Investigation

## Disks

Convert disk to RAW image

```bash
# From VMWare
qemu-img convert -f vmdk -O raw disk.vmdk disk.img
# From Virtualbox
qemu-img convert -f ova -O raw disk.vmdk disk.img
```

Unpack LVM

```bash
kpartx -a -v $DUMP.lvm2
```

## Docker containers

```bash
docker exec -it $CONTAINERNAME /bin/bash
```

## Tracks

### Other

Get hostname

```bash
/etc/hostname
```

Get timezone

```bash
/etc/timezone
```

### Network

List interfaces

```bash
cat /etc/network/interfaces
```

List actives connections

```bash
netstat -natp
```

List hardcoded dns

```bash
cat /etc/hosts
```

Get DNS settings

```bash
cat /etc/resolv.conf
```

### User/Groups/Rights

List users from `passwd`

```bash
cat /etc/passwd | column -t -s :
```

List sudoers

```bash
sudo cat /etc/sudoers
```

List groups

```bash
cat /etc/group
# Find users from a group
cat /etc/group | grep '$GROUPNAME'
```

### Persistant

#### Startup

```bash
ls /etc/init.d
ls /etc/profile.d
cat ~/.bashrc
```

#### Cron

List cron tasks

```bash
crontab -l
# Root
less /etc/crontab
# From a user
sudo crontab -u $USERNAME -l
# Hourly
ls -la /etc/cron.hourly/
# Daily
ls -la /etc/cron.daily/
# Weekly
ls -la /etc/cron.weekly/
# Montly
ls -la /etc/cron.montly/
```

### Logs

???+ tip "Manipulate logs"
    ```bash
    less -r $LOGFILE
    tail -n $LINES $LOGFILE
    ```

#### Auth

Last login

```bash
sudo last -f /var/log/wtmp
```

Auth

```bash
cat /var/log/auth.log | less -r
```

Bash history

```bash
cat /home/$USER/.bash_history | less -r
```

SSH Key

```bash
cat /home/$USER/.ssh/authorized_keys | less -r
```

### Proccessus

```bash
# Netcat detection
ps -aux | grep 'nc '
```

## Sources

- [Phoenixnap home contact support blog Glossary How to List, Display, & View all Current Cron Jobs in Linux](https://phoenixnap.com/kb/how-to-list-display-view-all-cron-jobs-linux)
