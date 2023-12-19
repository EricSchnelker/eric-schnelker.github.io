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
      $ ping -c 3 archlinux.org
```
-----------------------
5. #### Formatted a partition for EFI, a partition for FAT32 (Swap partition) and the linux filesystem (EXT4)
   * ###### List Disks
     ``` bash
         $ fdisk -l
     ```
   * ###### Create disk layout partition table
     ``` bash
         $ cfdisk /dev/sda
     ```
   * ###### Create FAT32 file system
     ``` bash
         $ mkfs.fat -F32 /dev/sda1
     ```
   * ###### Prepare the swap partition:
     ``` bash
         $ mkswap /dev/sda2
         $ swapon /dev/sda2
     ```
   * ###### Created EXT4 file system for root partition
     ``` bash
         $ mkfs.ext4 /dev/sda3
     ```
-----------------------
6. #### Sync pacman repository, then mount root partition to /mnt directory nstalled base packages before installing base packages
  * ###### Sync pacman repository
         ``` bash
              $ pacman -Syy
         ```
  * Mount root partition to /mnt directory
         ``` bashpacstrap -K /mnt base linux linux-firmware sudo nano
              $ mount /dev/sda3 /mnt
         ```
  * Install all necessary packages and nano
         ``` bash
              $ pacstrap -K /mnt base linux linux-firmware sudo nano
         ```
-----------------------
7. #### Generated /etc/fstab file
     ``` bash
          $ genfstab -U /mnt >> /mnt/etc/fstab
     ```
-----------------------
8. #### Chrooted into the install
    ``` bash
          $ arch-chroot /mnt
    ```
-----------------------
9. #### Used nano to modify locale-gen file and uncomment necessary locales, then ran locale-gen
-----------------------
12. #### Created and set the lang variable using echo and export
-----------------------
13. #### Set host name
-----------------------
14. #### Set root password
-----------------------
15. #### Installed grub and used it on sda1 (EFI partition)
-----------------------
16. #### Installed GNOME
-----------------------
17. #### Installed Xorg packages
-----------------------
18. #### Installed Nvidia packages
    * ###### Drivers
-----------------------
19. #### Installed GNOME and enabled GDM
-----------------------
20. #### Installed Network Manager and enabled the service
-----------------------
21. #### Installed vim
-----------------------
22. #### Created user EricSchnelker and set password
    * ###### Added user to wheel group
-----------------------
23. #### Changed sudoers file to give wheel group permission to sudo.
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
