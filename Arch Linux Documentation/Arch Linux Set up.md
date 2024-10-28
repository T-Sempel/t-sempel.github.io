1. Download ISO image, MIT
2.  The I booted up VM ware workstation
3. I created a new l VM machine using ARCH
4. I then expanded the memory two 2gb and the hard disk to 20gb
5. ![alt text](<Pasted image 20241027143633.png>)
6. I then went to the advance setting and changed the firm ware to UEFI
7. Once powerd on I was met with this screen
8. ![alt text](<Pasted image 20241027144148.png>)
9. ![alt text](<Pasted image 20241027144325.png>)
10. When recognized by the live system, disks are assigned to a [block device](https://wiki.archlinux.org/title/Block_device "Block device") such as `/dev/sda`, `/dev/nvme0n1` or `/dev/mmcblk0`. To identify these devices, use [lsblk](https://wiki.archlinux.org/title/Lsblk "Lsblk") or   fdisk_.fdisk -l
11. The I used fdisk /dev/sda
12. Then I typed g, n, 1, nad +500m
13. ![alt text](<Pasted image 20241027145130.png>)
14. I then typed t, n, 2, w
15. I am now on 1.10 of the Wiki
16. mkfs.ext4 /dev/sda2
17. mkfs.fat -F 32 /dev/sda1
18. ![alt text](<Pasted image 20241027145610.png>)
19. mount /dev/sda2 /mnt
20. mount --mkdir /dev/sda1 /mnt/boot
21. pacstrap -K /mnt base linux-firmware
22. ![alt text](<Pasted image 20241027150140.png>)
23. genfstab -U /mnt >> /mnt/etc/fstab
24. arch-chroot /mnt
25. # ln -sf /usr/share/zoneinfo/_Region_/_City_ /etc/localtime I set the time to America and Chicago
26. hwclock --systohc
27. ![alt text](<Pasted image 20241027151138.png>)
28. These are the commands used for the Localization
29. echo "arch" > /etc/hostname
30. I then set a password with passwd
31. I then went on to install grub.
32. ![alt text](<Pasted image 20241027154622.png>)
33. pacman -S lxqt
34. pacman -S sddm
35. systemctl enable sddm.service
36. Next I added the user justin and codi
37. I used useradd  justin, codi
38. Then changed their passwords
39. ![alt text](<Pasted image 20241027174801.png>)
40. I also added myself with useradd -m -G travis
I installed the following before rebooting:
pacman -S networkmanager
pacman -S nano
pacman -S vi
pacman -S zsh
pacman -S openssh
pacman -S sudo

I also changed the contents of /etc/sudoers using visudo. I uncommented the %wheel line to give sudo access to the users I previously established as being in the group wheel (justin, codi, travis)

To add color coding and aliases:
nano ~/.bashrc
Insert the following:
alias ls='ls --color=auto'
alias ll='ls -la'
alias l='ls -CF'
alias c='clear'
PS1='\[\e[1;32m\]\u@\h \[\e[1;34m\]\w\[\e[0m\] \$ '


I now type exit and reboot the VM to have the changes applied

Everything looks great, but I noticed that the icons were not showing on the desktop. To fix this, I opened the terminal and used the command sudo pacman -S papirus-icon-theme
There was an error installing it, so I used systemctl enable NetworkManager, systemctl start NetworkManager and I tried again to use pacman

This time it worked without problems, and the icons were fixed after I went to LXQt Configuration Center > Appearance > Icons Theme > Papirus

I noticed that the terminal did not have any changes to the color that I thought I applied earlier, so I opened ~/.bashrc again and it seemed to have a different format. I changed it to make it the way I intended. I then used the command source ~/.bashrc to make sure the changes were saved.
![alt text](<Pasted image 20241027204837.png>)