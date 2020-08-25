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

## 3.Configure `Android Debug Bridge(adb)`

>Gentmotion have installed and use `Genymotion Android Tools(default)` by default.

But your variable **$PATH** haven't included its path, so you need to configre **$PATH** by yourself.

```
export PATH=$PATH:/usr/local/share/applications/genymotion/tools
```

You can execute this command in your terminal but it only is valiable this time. You can add it at the end of **~/.bashrc** so that it could be valiable permanent for this user.

## 4.Increase Internel Storage of Genymotion Device

>Tip: Default size of Genymotion Virtual Device only has 16 GB. 

## 4.1 Increase physical disk size.

4.1.1 In **Oracle VM VirtualBox Manager**,you need to go to **Tools(Top of menu)--Media(Click rightest button of Tools Tab)**.

4.1.2 Copy **android_data_disk.vmdk** to a new **VDI(VirtualBox Disk Image)** type disk image named **android_data_disk_copy.vdi**.

4.1.3 Modify properties of **android_data_disk_copy.vdi**, then you could Change *size* and *apply*.

4.1.4 Copy `android_data_disk_copy.vdi` to a new `VMDK(Virtual Machine Disk)` type disk image named `android_data_disk_64gb.vdi`.

>Maybe you have increased the physical size of disk,But the filesystem doesn't extend to new size/block. You need to mount this new disk to other virtual machine system so that you can modify the filesystem.

## 4.2 Use `Live system` of *iso* file to increase filesystem size.

>Tip: Advise to use **Ubuntu** iso file to use Live system. 

4.2.1 New a Virtual Machine and set memory size.

4.2.2 Remember to choose **Use an existing virtual hard disk file** and set `android_data_disk_64gb.vdi(Normal,64.00GB)` to create.

4.2.3 Go to `Settings--Storage--Controller:IDE--Optical Drive` and choose your **iso** file.

4.2.4 Open the Virtual Machine and use Live System without Installing it.

4.2.5 Do blow commands

```
sudo passwd       #Configure root user password
su -              #Login in root user with password which you configured just now.
lsblk -pa         #Parameters means "all" and "path" and help you find which device needed to modify filesystem size
```

>Tip: Genymotion file system is ext file system.android_data_disk_64gb.vdi is usually in **/dev/sda3**

```
resize2fs /dev/sda3 <custom>G
```

4.2.6 In `Oracle VM VirtualBox Manager`,you need to go to `<GenymotionPhoneVirtualMachine>--Settings--Storage`. You need to **Remove Attachment** named **android_data_disk.vmdk** and then **Adds hard disk** named **android_data_disk_64gb.vdi** and apply it.

## 5.Install `ARM translation tools`

>Note
For legal reasons, we cannot provide any ARM translation tools nor links to them. However, you should be able to find them on the Internet.

>Important: 
If you want to install the application from Google Play Store, you have to install the ARM translation tools **before** installing the OpenGApps package.
Please note that there are no ARM translation tools for Android 10 for the moment.

You can find ARM_Translation_tools [here](https://github.com/m9rco/Genymotion_ARM_Translation)

Also, you need to use an ARM translation tool that matches the Android version of your instance!

## 6.Install `Google Mobile Service(GMS)`

Click `OpenGApps` button in right menu bar.

## 7.Speed up your Network with `Bridge` Network

## You need to go to `Edit` tab and change `Network mode` to `Bridge` 

## 8.Install `exfat` format filesystem support

```
dnf -y install fuse-exfat
dnf -y install exfat-utils
```

## 9.Unlock `BitLocker` of Windows 10

Open **Windows Explorer** and *right-click* on the **BitLocker encrypted drive**, and then choose **Unlock Drive** from the context menu.
>Tips:You maybe need to wait for a long time to finish decrypt operation.
