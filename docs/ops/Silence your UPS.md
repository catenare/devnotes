# Silence your UPS

## Verify that your machine can see the UPS

![](UPS%20USB%20Device.png)

## Install VirtualBox

- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- Also download and install the Virtual Box Extension Pack.

## Setup the Debian Box
* Install Debian
	* Download the net-install image for Debian - [NetInstall 10.2](http://ftp.is.co.za/debian-cd/current/amd64/iso-cd/debian-10.2.0-amd64-netinst.iso)
	* Open VirtualBox and create a new virtual machine. Setup as Debian 64 machine.
	* Start the machine and select the debian netinst iso image as the startup image. (VirtualBox should ask for the image).
	* Install Debian on your virtual box.
	* Restart the virtual machine.
* Install Guest Additions - based on [Instructions](https://www.techrepublic.com/article/how-to-install-virtualbox-guest-additions-on-a-gui-less-ubuntu-server-host/) & [How to install Virtual Box Guest Additions](https://superuser.com/questions/950431/how-to-install-virtual-box-guest-additions-on-debian)

![](Capture%20Additions.png)

  * Mount the Guest Additions Image - From the main menu, under Devices choose Insert Guest Additions CD Image.
  * Log in as root
  * `apt-get update`
  * `apt-get upgrade`
  * `apt-get install -y dkms build-essential` # Install the necessary dependencies
  * Install the Guest Additions
	  * `mount /dev/dvd` - Should see WARNING: device write-protected, mounted read only.
    * `cd /media/cdrom`
    * `sh ./VBoxLinuxAdditions.run` # run the installer
  * Reboot
  * Login as root.
  * Verify that Guest additions were installed.
	  * `modinfo vboxguest` - Should see details about the module.
## Install the Network UPS Tools - [Network Ups Tools](https://networkupstools.org)
* Verify that your UPS is supported - https://networkupstools.org/stable-hcl.html
* Connect your UPS to your computer using a USB cable.
* From the Virtual Machine Menu, See if your UPS is listed under Devices -> USB

![](Capture%20USB.png)

* `apt-get install nut` - install nut.
### Configure Network UPS Tools
* [Detailed NUT Configuration](https://wiki.ipfire.org/addons/nut/detailed)
* [HOWTO:](http://tedfelix.com/software/nut-network-ups-tools.html)
* Configure MODE - **nut.conf**
```
MODE=standalone
```

* Configure the UPS setup - **ups.conf**

```
[myups]
	driver = usbhid-ups
	port = auto
	desc = "My ups"
```

* Test with `upsdrvctl start`
* Configure the daemon **upsd.conf**

```
LISTEN 127.0.0.1 3493
```

* Configure **upsd.users**

```
[admin]
	password = pass
	actions = SET
	instcmds = ALL
	upsmon master
```

* Start daemon - `upsd`
* Read status - `upsc myups@localhost`
* See which commands are available - `upscmd -l myups@localhost`
* Disable the Beep - [Disable the beep from your device](https://linux-tips.com/t/disabling-ups-beep-under-linux/592)
* Disable the beep - 

```
upscmd myups@localhost beeper.disable
Username: admin
Pasword: pass
```
