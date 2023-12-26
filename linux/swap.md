# Increase Swap AWS micro

Check filesystem to see if swapfile is supported (ext3 ext4 xfs) check for others.

```shell
lsblk -f
```

Determine the swapfile space need. `if ram <= 1GB -> 1GB swap`. `If ram > 1GB -> swap >= √ram`

```shell
free -hm
```

*bs* = block size *count* = number of blocks amount of ram = block size \* count

```shell
sudo dd if=/dev/zero of=/swapfile bs=128M count=8
```

Update read/write permissions

```shell
sudo chmod 600 /swapfile
```

Set the linux swap area

```shell
sudo mkswap /swapfil
```

Check if was successfull

```shell
sudo swapon /swapfile
```

```shell
sudo swapon -s

```

Start at boot

```shell
sudo nano /etc/fstab
```

```shell
/swapfile swap swap defaults 0 0
```
