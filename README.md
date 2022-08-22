# Cheat sheet for exam EX200 - Red Hat Certified System Administrator

## SELinux

### Operational mode

```bash
getenforce
sudo setenforce 0|1
```

```
vi /etc/selinux/config
```

### List & manage context
```
ls -ltZ
ps -aZ
ps -ZC httpd
ps -U root -Z
```




