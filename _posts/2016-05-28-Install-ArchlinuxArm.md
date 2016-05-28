Note: The current installation uses the 32-bit Raspberry Pi 2 armv7h root filesystem. This will be changing eventually to use our AArch64 repository to take full advantage of the ARMv8 Cortex-A53 cores. If you want an AArch64 system, consider the ODROID-C2.

Also note: The Raspberry Pi 3 has higher power requirements than the Raspberry Pi 2. A power supply rated at 2.5A is the official recommendation. Using an insufficient power supply will result in random, inexplicable errors and filesystem corruption.

Replace sdX in the following instructions with the device name for the SD card as it appears on your computer.
### Install System

1. Start fdisk to partition the SD card:
	`fdisk /dev/sdX`
2. At the fdisk prompt, delete old partitions and create a new one:
    Type o. This will clear out any partitions on the drive.
    Type p to list partitions. There should be no partitions left.
    Type n, then p for primary, 1 for the first partition on the drive, press ENTER to accept the default first sector, then type +100M for the last sector.
    Type t, then c to set the first partition to type W95 FAT32 (LBA).
    Type n, then p for primary, 2 for the second partition on the drive, and then press ENTER twice to accept the default first and last sector.
    Write the partition table and exit by typing w.
3. Create and mount the FAT filesystem:
    `mkfs.vfat /dev/sdX1`
    `mkdir boot`
    `mount /dev/sdX1 boot`
4. Create and mount the ext4 filesystem:
    `mkfs.ext4 /dev/sdX2`
    `mkdir root`
    `mount /dev/sdX2 root`
5. Download and extract the root filesystem (as root, not via sudo):
    wget http://archlinuxarm.org/os/ArchLinuxARM-rpi-2-latest.tar.gz
    bsdtar -xpf ArchLinuxARM-rpi-2-latest.tar.gz -C root
    sync
6. Move boot files to the first partition:
	mv root/boot/* boot
7. Unmount the two partitions:
	umount boot root 
8. Insert the SD card into the Raspberry Pi, connect ethernet, and apply 5V power.
9. Use the serial console or SSH to the IP address given to the board by your router.
Login as the default user alarm with the password alarm.
The default root password is root.

### Power on and setup
1. Login:
	`user: root password: root`
2. delete the alarm user
	`userdel alarm`
3. add user
	`useradd -m -g users -G wheel.power,audio,video,uucp,lp,adm -s /bin/bash 			username`
4. change the user password
	`passwd username`
5. Update system
	`pacman -Syy`
    `pacman -Syu`
6. Install vim text editor
	`pacman -S vim`
7. Change the mirrorlist
	`vim /etc/pacman.d/mirrorlist`
    `中科大的源`
    `Server = http://mirrors.ustc.edu.cn/archlinuxarm/$arch/$repo`
    `清华大学的源`
    `Server = http://mirrors.tuna.tsinghua.edu.cn/archlinuxarm/$arch/$repo`
8. Update
	`pacman  -Syy`
9. Install xdg-user-dirs在home目录下生成文件夹
	`pacman -S xdg-user-dirs`
10. Install sudo and change the `/etc/sudoers` file
	`pacman -S sudo`
    `vim /etc/sudoers`
    uncomment the following line:
    `#%wheel ALL=(ALL) ALL`
11. reboot
12. Install Qt library
	`pacman -S qt5 qt5-base` enter the default
13. Install mysql
	`pacman -S mysql` enter the default
14. Change the localtime 
	`sudo ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime`
15. Change the locale-gen
	uncomment the following line
    ```
    en_US.UTF-8
    en_US ISO-8859-1
    zh_CN.UTF-8
    zh_CN GB2312
    ```
    then excute `sudo locale-gen`
16. Create new file in `/etc/locale.conf` and add the following line
	`LANG=en_US.UTF-8`
    then soure the new file
    `source /etc/locale.conf`
17.	Install Wireless 
	`sudo pacman -S wpa_supplicant wpa_actiond dialog ppp ifplugd dhcpcd`
    `sudo wifi-menu` to search wireless to connect
    enable the wireless automatically connect:
    `sudo systemctl enable netctl-auto@wlan0.service`

18. excute the application ./appname

OK, It's Done.