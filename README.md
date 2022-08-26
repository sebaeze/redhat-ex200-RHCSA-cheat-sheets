# Cheat sheet for exam EX200 - Red Hat Certified System Administrator

## Tune System Performance

### Killing processes

#### Listing available SIGNs
```
kill -L  
```

#### Searching and killing job
```
jobs 
kill -SIGSTOP %3
```

#### Listing user and log-out
```
w
pkill -SIGKILL -u other_user
```

### Monitor activity

####
```
uptime
top
lscpu
```

## SELinux

### Operational mode

```bash
getenforce
sudo setenforce 0|1
```

```
vi /etc/selinux/config
```

### List context
```
ls -ltZ
ps -aZ
ps -ZC httpd
ps -U root -Z
```

### Manage File Context

#### List all fcontext
```
sudo semanage fcontext -l
```
#### List fcontext of current path
```
sudo semanage fcontext -l -C
```
#### Add file context
```
sudo ls -Z /home/user/*
sudo semanage -a -t default_t "/home/user(/.*)?"
sudo restorecon -R -v /Home/user
sudo ls -Z /home/user/*
```
#### Delete file context
```
sudo semanage -d "/home/user(/.*)?"
sudo restorecon -R -v /Home/user
```


### SELinux Booleans

```
getsebool -a 
semanage boolean -l
```

```
setsebool httpd_anon_write=1
```

## Troubleshooting

```
egrep -i 'sealert' /var/log/messages
sealert -l 82611f98-6b56-63bc-23da-c4791c9a9ab7
```
