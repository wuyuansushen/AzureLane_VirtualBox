## Deploy Azure Lane Bot to run Script

## 1.Install *Virtual Box*

## 1.1 Close ***Secure Boot*** in your motherboard.

## 1.2 Close ***SELinux***

>Selinux and VirtualBox
ATM, we don't support running VirtualBox with selinux enabled, solution is disable selinux.

Check your Linux SELinux status

```
sestatus
```

If your SELinux type is *enforcing*, you should

```
setenforce 0 #It means change enforcing to permissive
```
and set 
```
SELINUX=permissive
```
in */etc/selinux/config* so that the change will be permanent.
