---
title: Raspberry PI Admin
updated: 2021-06-20 17:05:16Z
created: 2021-03-07 14:27:28Z
---

## Rclone
### Copy files from storage hdd to OneDrive
* Using rclone - https://rclone.org
#### Install rclone on dev pi
* Will need to get the token on a machine with a browser
* rclone config for OneDrive - https://rclone.org/onedrive/
* `rclone authorize onedrive`
* `sudo apt install rclone`
* `rclone config`
	* n - New remote
	*  Microsoft OneDrive - Type of storage
	* Microsoft App Client ID - leave blank
	* Microsoft App Client Secret - leave blank
	* Choose Microsoft Cloud Global
	* Choose - OneDrive for Personal or Business
	* Select the drive you want to use (0 in my case)

* Quota available
	* `rclone about OneDrive: `
```
Total:   1.005T
Used:    84.698G
Free:    944.302G
Trashed: 91.924k
```

#### Mount external hdd on Ubuntu
* `lsblk` - see if drive is listed
```
NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
loop0         7:0    0  48.5M  1 loop /snap/core18/1883
loop1         7:1    0  48.9M  1 loop /snap/core18/1990
loop2         7:2    0    63M  1 loop /snap/lxd/19573
loop3         7:3    0    63M  1 loop /snap/lxd/19390
loop4         7:4    0    27M  1 loop /snap/snapd/11043
loop5         7:5    0    26M  1 loop /snap/snapd/8543
loop6         7:6    0 104.3M  1 loop /snap/docker/800
sda           8:0    0 931.5G  0 disk
├─sda1        8:1    0   200M  0 part
└─sda2        8:2    0 931.2G  0 part
mmcblk0     179:0    0  59.5G  0 disk
├─mmcblk0p1 179:1    0   256M  0 part /boot/firmware
└─mmcblk0p2 179:2    0  59.2G  0 part /
```

* Want to mount sda2 /dev/sda2
* `sudo fdisk -l` - Type of the devices
```
Disk /dev/sda: 931.49 GiB, 1000170586112 bytes, 1953458176 sectors
Disk model: My Passport 0820
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: A17712B3-71DC-4432-81AC-17AC305F1D4D

Device      Start        End    Sectors   Size Type
/dev/sda1      40     409639     409600   200M EFI System
/dev/sda2  409640 1953195991 1952786352 931.2G Apple HFS/HFS+
```

* `mkdir ~/BackupDisk`
* `sudo mount /dev/sda2 ~/BackupDisk` - Able to mount Apple HFS systems without additional parameters

* HFS drive as rw - does not work for journalled file
	* https://askubuntu.com/questions/332315/how-to-read-and-write-hfs-journaled-external-hdd-in-ubuntu-without-access-to-os
	* Try to setup as RW
	* `sudo mount -t hfsplus -o force,rw /dev/sda2 ~/BackupDisk`
	* `sudo fsck.hfsplus /dev/sda2`

* Want to copy **~/StorageDisk/images** to **OneDrive/BackupDrive**
* Start tmux on Raspberry PI - `tmux`
* `rclone copy ~/BackupDisk/images OneDrive:BackupDrive -Pv`
* Will log in later to see the progress
## Format a Harddrive
* https://tecadmin.net/format-usb-in-linux/
* `sudo mkfs.ext4 /dev/sda`
## Update bootloader
### Raspberry PI Update
* Update Raspberry pi bootloader
	* https://www.raspberrypi.org/documentation/hardware/raspberrypi/bcm2711_bootloader_config.md
	* `sudo apt install libraspberrypi-bin`
	* `vcgencmd bootloader_version` - check bootloader version
	* `sudo apt install rpi-eeprom -y` - program to install eeprom upgrade
	* `sudo rpi-eeprom-update` - see if update available
	* `sudo rpi-eeprom-update -a` - update eeprom
	* Update boot config - https://www.raspberrypi.org/documentation/hardware/raspberrypi/bcm2711_bootloader_config.md
	* `sudo -E rpi-eeprom-config --edit`
		* Changed **BOOT_ORDER** to boot **0x5** for USB2.0 boot
## Setup SSH authentication
### What worked - For Lightsail Server
* `ssh-keygen` - created default key pair
* `ssh-add LightsailDefaultKey-eu-central-1.pem`
* `ssh-copy-id -i ~/.ssh/id_rsa ubuntu@api.paseo.org.za` - copied the file over
* `ssh-copy-id -i ~/.ssh/id_rsa ubuntu@192.168.100.120` - Raspberry PI Server
* `ssh-copy-id -i ~/.ssh/id_rsa pi@192.168.100.100` - PiHole server and UPS monitor
## Installing Docker and Portainer on Ubuntu
* https://snapcraft.io/install/docker/ubuntu
* https://documentation.portainer.io/v2.0/deploy/ceinstalldocker/ - portainer
	* `docker volume create portainer_data`
	* `docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce`
* Home Assistant - https://www.home-assistant.io/installation/raspberrypi#install-home-assistant-container
* `docker volume create homeassistant_data`
```
docker run --init -d --name homeassistant -p 8123:8123 --restart=unless-stopped -v /etc/localtime:/etc/localtime:ro -v homeassistant_data:/config --network=host homeassistant/raspberrypi4-homeassistant:stable
```
* Add node-red
* https://nodered.org/docs/getting-started/docker#running-headless
* `docker volume create node_red_data`
	* `docker run -d -p 1880:1880 -v node_red_data:/data --name hanodered nodered/node-red:latest`

* Free ddns service. Signed in with sfbushie@gmail.com with google
* https://www.duckdns.org/domains
* `sahomeserver.duckdns.org`
* Waveshare Display - https://www.waveshare.com/wiki/7.9inch_HDMI_LCD
* https://www.waveshare.com/product/displays/lcd-oled/lcd-oled-1/7.9inch-hdmi-lcd.htm