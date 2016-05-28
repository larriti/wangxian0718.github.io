---
layout: post
title: install Archlinux
date: 2016-05-20T14:37:44.000Z
---
##Install Archlinux ArchWay

1. `pacman -Syy`
2. `pacman -S reflector`
3. `reflector -c 'China' -f 12 -l 12 -n 12 --verbose --save /etc/pacman.d/mirrorlist`
4. `fdisk /dev/sdX `
5. `mkfs.ext4  /devsdX1`
6. `mkfs.ext4  /dev/sdX2`
7. `mkswap	/dev/sdX3`
8. `mount /dev/sdX1 /mnt`
9. `mkdir /mnt/root(or mkdir /mnt/home)`
10. `mount /dev/sdX2 /mnt/boot (or /mnt/home)`
11. `swapon /dev/sdX3`
12. `pacstrap /mnt base base-devel`
13. `genfstab -U -p /mnt >> /mnt/etc/fstab`
14. `arch-chroot /mnt`
15. `passwd`
16. `vim /etc/locale.gen`
17. `uncomment the en_US.UTF-8 en_US.ISO-8859-1`
18. `locale > /etc/locale.conf`
19. `ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime`
20. `useradd -m -g users -G wheel,lp,power,audio,video,storage,adm -s /bin/bash newusername`
21. `passwd newusername`
22. `vim /etc/sudoers`
23. `echo vbox > /etc/hostname`
24. `vim /etc/hosts (change the localhost to your username)`
25. `systemctl enable dhcpcd.service`
26. `pacman -S wireless_tools wpa_supplicant dialog net-tools`
27. `pacman -S reflector rsync mlocate bash-completion`
28. `pacman -S virtualbox-guest-utils`
29. `pacman -S linux-headers`
30. `systemctl enable vboxservice.service`
31. `pacman -S xf86-video-(intel ati nvdia)`
33. `pacman -S alsa-utils`
32. `pacman -S xfce4`
33. `pacman -S xorg-xinit xorg-twm xorg-xclock xterm `
34. `mkinitcpio -p linux`
35. `pacman -S grub os-prober`
36. `grub-install /dev/sdX`
37. `grub-mkconfig -o /boot/grub/grub.cfg`
38. `ctrl+D to exit`
39. `umount /mnt -R`
40. `poweroff(or reboot)`
41. `pacman -S wqy-zenhei`
