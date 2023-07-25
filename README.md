# IterkoczeOS
Official Iterkocze Operating system

## Installation
When it comes to installation, you have two options. <br>
Either using the official installation medium and using the automated script within it (recommended for quick VM installs) <br>

<b>or</b> <br>

Downloading the raw system build and installing it manually (recommended for installing on a physical computer)

### Note about installing IterkoczeOS in a VM
IterkoczeOS is currently only supported in VirtualBox with specific settings. Make sure your VM with IterkoczeOS has the following settings before proceeding with installation <br>
Settings -> System -> Motherboard -> Pointing Device -> USB Tablet <br>
Settings -> Display -> Screen -> Graphics Controller -> VBoxVGA <br>

### Installation using the official installation medium
Download `iterkoczeos.iso` from https://drive.google.com/drive/folders/1jJ1n8cgSfiPi_KQ2M1Nb8i3q0ViWX7Ed?usp=sharing <br>
It's a netinstaller for IterkoczeOS

Boot up the ISO and login using
```
username: root
password: 123
```
Download the raw build of IterkoczeOS using `links iterkoczeos.xlx.pl` <br>
Make sure that the downloded raw build is named `iterkoczeos.tar.xz`<br>
Run the installation script `./os-install` and follow the instructions provided <br>

### Manual installation 
For a manual installation, you need to have a working Linux environment set up. Whether it be a live CD or yor own installation <br>
In this example I'm using Arch live CD<br>
Boot up/prepare your environment and make sure you have:
- tar and xz
- fdisk
- GRUB
- About 6 GB of free drive space minimum
- About 1 GB of free RAM
- Working keyboard is also a nice thing to have for QOL (you don't need a mouse)
- Proper VM settings, if using one

All commands are ran as root <br>
Prepare your root partition and if desired, a swap partition using: <br>
```
fdisk /dev/XXX (replace XXX with your device identifier)
n
p
1
<Enter>
<Enter>
a
w

mkfs.ext4 /dev/XXXX (Replace XXXX with your device and partition identifier)
mount /dev/XXXX /mnt
cd /mnt
pacman -Sy links
links https://iterkoczeos.xlx.pl
tar -xvpf <system_tarball>
rm <system_tarball>
grub-install --boot-directory=/mnt/boot /dev/XXXX
vim etc/fstab (edit it to your needs)
```

Bind /dev using `mount -v --bind /dev /mnt/dev` <br>
And chroot `chroot /mnt` <br>
Configure the bootloader using `grub-mkconfig -o /boot/grub/grub.cfg` <br>

<s>Now, you have to make the GRUB config file. To do that, put this in `/boot/grub/grub.cfg`
```
menuentry "IterkoczeOS" {
  root=hdX,msdos1
  linux /boot/vmlinuz-6.1.11-IterkoczeOS root=/dev/XXXY (XXX being your device, and Y being the partition number)
}
```
</s>

Network configuration has to be done before you boot into IterkoczeOS
```
ip link show
vim /etc/sysconfig/ifconfig.enp6s0
Change the network interface to the correct one shown by ip link show
```

Now you can reboot the system and boot into IterkoczeOS.

Boot up, select "IterkoczeOS" in the GRUB boot menu, log in as `user` with the default password of `123` and execute `startx`.

Also do not forget to read `README` in your user's home directory
