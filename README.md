# Cheat sheet for exam EX200 - Red Hat Certified System Administrator

## Tune System Performance


```
kill -L  
jobs 
kill -SIGSTOP %3
w
pkill -SIGKILL -u other_user
uptime
top
lscpu
```

## SELinux

```
getenforce
sudo setenforce 0|1
vi /etc/selinux/config
ls -ltZ
ps -aZ
ps -ZC httpd
ps -U root -Z
sudo semanage fcontext -l
sudo semanage fcontext -l -C
sudo ls -Z /home/user/*
sudo semanage -a -t default_t "/home/user(/.*)?"
sudo restorecon -R -v /Home/user
sudo ls -Z /home/user/*
sudo semanage -d "/home/user(/.*)?"
sudo restorecon -R -v /Home/user
getsebool -a 
semanage boolean -l
setsebool httpd_anon_write=1
```

## Repositories and SW packages

```
subscription-manager register --username nnnn 
subscription-manager list --available
subscription-manager list --consumed
subscription-manager attach
subscription-manager unregister
```

```
dnf list 'net*' | less
dnf search     'mongodb'
dnf search all 'mongodb'
dnf info   cups
dnf provides /bin/lp.cups
dnf install -y cups
dnf remove     cups
dnf update
dnf list kernel
dnf group list
dnf group install "xxxxxx"
dnf history
dnf repolist all
dnf config-manager --enable  my-repo-id-rpms
dnf config-manager --disable my-repo-id-rpms
dnf config-manager --add-repo="https://www.repo.id/ss"
cd /etc/yum.repos.d
```

```
rpm 
```

## Storage

```
cat /etc/fstab
lsblk -fp
mount /dev/dva4 /home/my_dir
mount uuid="xxxx-xxxx-xxxx-xxx" /home/my_dir
umount /home/my_dir
lsof
```

```
parted -l /dev/vdb
parted /dev/vdb unit s print
parted /dev/vdb mklabel msdos
parted /dev/vdb mklabel gpt
parted /dev/vdb mkpart  primary xfs 2048s 1000MB
udevadm settle
sudo vi /etc/fstab    <-- for persistent mount filesystem
sudo systemctl daemon-reload
sudo reboot
parted /dev/vdb mkpart primary xfs 2048s 1001MB
udevadm settle
mkfs.xfs /dev/vdb1  <--- format partition
mount | egrep -i 'my_dir'
```

```
parted /dev/vdb  mkpart  swap-name-part linux-swap 1001MB 1257MB
udevadm settle
swapoff /dev/vdb2
mkswap /dev/vdb2
free
swapon  /dev/vdb2
free
swapon --show
lsblk -fs /dev/vdb2
echo "UUID=xxxxxx-xxxxx-xxxx swap swap defaults 0 0" >> /etc/fstab
swapon -a
sudo systemctl daemon-reload
sudo systemctl reboot
```

## Troubleshooting

```
egrep -i 'sealert' /var/log/messages
sealert -l 82611f98-6b56-63bc-23da-c4791c9a9ab7
```
