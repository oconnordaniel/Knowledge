Dans-Arch-Laptop

sfdisk /dev/sda < sda.dump

Aliases:
   linux          
   swap           
   home           
   uefi           
   raid           
   lvm  
   
Arch install via DistroTube:

Using fdisk:
fdisk -l   (lists out the partitions)
fdisk /dev/sda  
In fdisk, "m" for help
In fdisk, "o" for DOS partition or "g" for GPT
In fdisk, "n" for add new partition
In fdisk, "p" for primary partition (if using MBR instead of GPT)
In fdisk, "t" to change partition type
In fdisk, "w" (write table to disk)

Make filesystem:
mkfs.fat -F32 /dev/sda1
mkswap /dev/sda2
swapon /dev/sda2
mkfs.ext4 /dev/sda3

Base Install:
mount /dev/sda3 /mnt (mounts it to mnt on live image)
pacstrap /mnt base linux linux-firmware
genfstab -U /mnt TWO GREATER THAN SIGNS /mnt/etc/fstab (YouTube doesn't allow angle brackets)

Chroot:
arch-chroot /mnt (change into root directory of our new installation)
ln -sf /usr/share/zoneinfo/REGION/CITY /etc/localtime
hwclock --systohc (sets the hardware clock)
pacman -S nano
nano /etc/locale.gen
locale-gen
nano /etc/hostname
nano /etc/hosts

Users and passwords:
passwd (set root pass)
useradd -m username (make another user)
passwd username (set that user's password)
usermod -aG wheel,audio,video,optical,storage username

Sudo:
pacman -S sudo
EDITOR=nano visudo

GRUB:
pacman -S grub
pacman -S  efibootmgr dosfstools os-prober mtools (if doing UEFI)
mkdir /boot/EFI (if doing UEFI)
mount /dev/sda1 /boot/EFI  #Mount FAT32 EFI partition (if doing UEFI)
grub-install --target=x86_64-efi  --bootloader-id=grub_uefi --recheck (if doing UEFI)
grub-mkconfig -o /boot/grub/grub.cfg

Networking:
pacman -S networkmanager
systemctl enable NetworkManager

Reboot:
exit the chroot by typing "exit"
umount /mnt (unmounts /mnt)
reboot (or shutdown now if doing this in VirtualbBox)
Remember to detach the ISO in VirtualBox before reboot.

