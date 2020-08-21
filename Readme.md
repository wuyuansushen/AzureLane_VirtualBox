## Deploy Azure Lane Bot to run Script

## 1.Install *Virtual Box*

## 1.1 Close `Secure Boot` in your motherboard.

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

## 1.3 Add `rpmfusion` repository

```
sudo dnf install https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
```

## 1.4 Install VirtualBox and Reload modules
```
sudo dnf install VirtualBox kernel-devel-$(uname -r) akmod-VirtualBox
sudo akmods
sudo systemctl restart systemd-modules-load.service
```

## 2.Install Genymotion
