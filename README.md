# IterkoczeOS
Official Iterkocze Operating system

## Installation
Head to: https://drive.google.com/drive/folders/1jJ1n8cgSfiPi_KQ2M1Nb8i3q0ViWX7Ed?usp=sharing <br>
for system tarballs.

In order to install IterkoczeOS, you will need a functioning Linux environment. 
Live CD will work too. If you are going with the Live CD idea, it's best to download plain Arch Linux as it's small.

Next, boot up/prepare your environment and make sure you have:
- tar and xz
- fdisk
- GRUB
- About 6 GB of free drive space minimum
- About 1 GB of free RAM
- Working keyboard is also a nice thing to have for QOL (you don't need a mouse)

Prepare your root partition and if desired, a swap partition using (all commands below are run as root):
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
```

Now, you have to make the GRUB config file. To do that, put this in `/boot/grub/grub.cfg`
```
menuentry "IterkoczeOS" {
  root=hd0,msdos1
  linux /boot/vmlinuz-6.1.11-IterkoczeOS root=/dev/sda1
}
```

Now you can reboot the system and boot into IterkoczeOS.
