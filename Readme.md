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

you also can check VirtualBox kernel module status:
```
dmesg | grep -i vboxdrv
```

## 2.Install Genymotion

## 2.1 Go to Genymotion Official Website to Download

Download page is [here](https://www.genymotion.com/download/)

## 2.2 Run the file and select installation path

```
chmod u+x <Genymotion>.bin
./<Genymotion>.bin -d <InstallPath>
```

## 3.Install `Android SDK package(adb)`

```
sudo dnf install android-tools
```

## 4.Install `ARM translation tools`

>Note
For legal reasons, we cannot provide any ARM translation tools nor links to them. However, you should be able to find them on the Internet.

>Important: 
If you want to install the application from Google Play Store, you have to install the ARM translation tools **before** installing the OpenGApps package.
Please note that there are no ARM translation tools for Android 10 for the moment.

You can find ARM_Translation_tools [here](https://github.com/m9rco/Genymotion_ARM_Translation)

Also, you need to use an ARM translation tool that matches the Android version of your instance!

## 5.Install `Google Mobile Service(GMS)`

Click `OpenGApps` button in right menu bar.

## 6.Speed up your Network with `Bridge` Network

## You need to go to `Edit` tab and change `Network mode` to `Bridge` 

## 7.Install `exfat` format filesystem support

```
dnf -y install fuse-exfat
dnf -y install exfat-utils
```
