#Install Archlinux ArchWay

1. pacman -Syy
2. pacman -S reflector
3. reflector -c 'China' -f 12 -l 12 -n 12 --verbose --save /etc/pacman.d/mirrorlist
4. fdisk /dev/sdX 
5. mkfs.ext4  /devsdX1
6. mkfs.ext4  /dev/sdX2
7. mkswap	/dev/sdX3
8. mount /dev/sdX1 /mnt
9. mkdir /mnt/root(or mkdir /mnt/home)
10. mount /dev/sdX2 /mnt/boot (or /mnt/home)
11. swapon /dev/sdX3
12. pacstrap /mnt base base-devel
13. genfstab -U -p /mnt >> /mnt/etc/fstab
14. arch-chroot /mnt
14. passwd
15. vim /etc/locale.gen
16. uncomment the en_US.UTF-8 en_US.ISO-8859-1
17. locale > /etc/locale.conf
18. ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
19. useradd -m -g users -G wheel,lp,power,audio,video,storage,adm -s /bin/bash ***newuser***
20. passwd ***newuser***
21. vim /etc/sudoers
22. echo vbox > /etc/hostname
23. vim /etc/hosts (change the localhost to your username)
24. systemctl enable dhcpcd.service
25. pacman -S wireless_tools wpa_supplicant dialog net-tools
26. pacman -S reflector rsync mlocate bash-completion
27. pacman -S virtualbox-guest-utils
28. pacman -S linux-headers
28. systemctl enable vboxservice.service
29. pacman -S xf86-video-(intel ati nvdia)
30. pacman -S alsa-utils
31. pacman -S xfce4
32. pacman -S xorg-xinit xorg-twm xorg-xclock xterm 
32. mkinitcpio -p linux
33. pacman -S grub os-prober
34. grub-install /dev/sdX
35. grub-mkconfig -o /boot/grub/grub.cfg
36. ctrl+D to exit
37. umount /mnt -R
38. poweroff(or reboot)
39. pacman -S wqy-zenhei  
