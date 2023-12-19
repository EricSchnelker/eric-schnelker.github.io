    Eric Schnelker
    Codi West
    System Administration
    12/8/2023
## <ins><p style="text-align: center;">Arch Linux -- Install Documentation</ins></p>
1. #### Acquired Arch Linux .iso from mirror link provided by the Arch Linux wiki
   * ###### Used MIT mirror to download
-----------------------
2. #### Set-up Arch VM in VMware Workstation Pro using the VM setup wizard and the .iso
   * ###### Configured memory and partition size while doing so
-----------------------
3. #### Connected to wifi
   * ###### Virtual ethernet connection from vm to host, host using TUwireless wifi
-----------------------
4. #### Pinged the Arch Linux Website
``` bash
      ping -c 3 archlinux.org
```
-----------------------
5. #### Formatted a partition for EFI, a partition for FAT32 (Swap partition) and the linux filesystem (EXT4)
   * ###### List Disks
     ``` bash
         fdisk -l
     ```
   * ###### Create disk layout partition table
     ``` bash
         cfdisk /dev/sda
     ```
   * ###### Create FAT32 file system
     ``` bash
         mkfs.fat -F32 /dev/sda1
     ```
   * ###### Prepare the swap partition:
     ``` bash
         mkswap /dev/sda2
         swapon /dev/sda2
     ```
   * ###### Created EXT4 file system for root partition
     ``` bash
         mkfs.ext4 /dev/sda3
     ```
-----------------------
6. #### Sync pacman repository, then mount root partition to /mnt directory nstalled base packages before installing base packages
  * ###### Sync pacman repository
     ``` bash
         pacman -Syy
     ```
  * Mount root partition to /mnt directory
     ``` bash
         mount /dev/sda3 /mnt
     ```
  * Install all necessary packages and nano
     ``` bash
         pacstrap -K /mnt base linux linux-firmware sudo nano
     ```
-----------------------
7. #### Generated /etc/fstab file
     ``` bash
         genfstab -U /mnt >> /mnt/etc/fstab
     ```
-----------------------
8. #### Chrooted into the install
     ``` bash
         arch-chroot /mnt
     ```
-----------------------
9. #### Set the timezone
    ``` bash
         ln -sf /usr/share/zoneinfo/America/Chicago /etc/localtime
    ```
-----------------------
10. #### Used nano to modify locale-gen file and uncomment necessary locales, then ran locale-gen
  * ###### Create and modify locale-gen file using nano
    ``` bash
         nano /etc/locale.gen
    ```
  * ###### Run locale-gen
    ``` bash
         locale-gen
    ```
-----------------------
11. #### Synchronize the hardware clock
    ``` bash
         hwclock --systohc
    ```
-----------------------
12. #### Created and set the lang variable using echo and export
    ``` bash
        echo LANG=en_US.UTF-8 > /etc/locale.conf
        export LANG=en_US.UTF-8
    ```
-----------------------
13. #### Set hostname and add to /etc/hosts file using nano
  * ###### Set hostname
    ``` bash
         echo arch-pc > /etc/hostname
    ```
  * ###### Add hostname to /etc/hosts file
    ``` bash
         nano /etc/hosts
    ```
-----------------------
14. #### Set root password
    ``` bash
         passwd
    ```
-----------------------
15. #### Installed GRUB bootloader, EFI Boot Manager and used it on sda1 (EFI partition)
  * ###### Installed GRUB bootloader package as well as EFI Boot Manager package
    ``` bash
         pacman -S grub efibootmgr os-prober mtools
    ```
  * ###### Create mount point for /dev/sda1 and mount it
    ``` bash
         mkdir /boot/efi
         mount /dev/sda1 /boot/efi
    ```
  * ###### Install bootloader
    ``` bash
         grub-install --target=x86_64-efi --bootloader-id=grub_uefi
    ```
  * ###### Finally, generate the “/boot/grub/grub.cfg” file.
    ``` bash
         grub-mkconfig -o /boot/grub/grub.cfg
    ```
-----------------------
16. #### Installed Xorg packages
    ``` bash
         pacman -S xorg-server xorg-apps
    ```
-----------------------
17. #### Installed Nvidia packages
    ``` bash
         pacman -S nvidia nvidia-utils
    ```
-----------------------
18. #### Installed GNOME and enabled GDM as well as Network Manager
  * ###### Install GNOME
    ``` bash
         systemctl enable gdm
    ```
  * ###### Enable GDM, then enable NetworkManager
    ``` bash
         systemctl enable NetworkManager
    ```
-----------------------
19. #### Created user EricSchnelker, set password, and added user to wheel group
  * ###### Create user and add to wheel group
    ``` bash
         useradd -m -G wheel EricSchnelker
    ```
  * ###### Set passwd for new user
    ``` bash
         passwd EricSchnelker
    ```
-----------------------
20. #### Changed sudoers file to give wheel group permission to sudo.
  * ###### Open the visudo file using nano
     ``` bash
         EDITOR=nano visudo
    ```
  * ###### Find the following line
    ``` bash
         # %wheel ALL=(ALL) ALL
    ```
  * ###### Uncomment it by removing the # sign
     
-----------------------
24. #### Created user codi and set password to GraceHopper1906 and set it to force a password change at next login
    * ###### Added codi to wheel group, giving sudo permissions
-----------------------
25. #### Installed zsh
-----------------------
26. #### Installed openssh
    * ###### Started service and enabled it to start at runtime
-----------------------
27. #### Installed yay-git AUR
-----------------------
28. #### Installed chrome using yay
-----------------------
29. #### Modified .bashrc using nano to add colors to the terminal
-----------------------
30. #### Added .bash_aliases and a script into .bashrc to read aliases from .bash_aliases
    * ###### Added alias for exit (e)
    * ###### Added alias for clear (c)
    * ###### Added alias for ls -a (l)
    * ###### Added alias to allow for copy to have a progress bar (cpv)
-----------------------
31. #### Already installed a bootloader, would rather have it boot into that in case of any future issues with GNOME than directly booting into GNOME.
