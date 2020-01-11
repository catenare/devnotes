# Silence your UPS

- For Mac OS X, we need to setup a Linux virtual machine.

## Install VirtualBox

- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- Also downlaod and install the _Virtual Box Extension Pack._

## Setup Debian Virtual Machine

- Download the net-install image for Debian - [NetInstall 10.2](http://ftp.is.co.za/debian-cd/current/amd64/iso-cd/debian-10.2.0-amd64-netinst.iso)
- Open _VirtualBox_ and create a new virtual machine. Setup as Debian 64 machine.
- Start the machine and select the _debian netinst_ iso image as the startup image. (VirtualBox should ask for the image).
- Install Debian on your virtual box.

* Restart the virtual machine.

- Install the Guest Additions - Based on [Instructions](https://www.techrepublic.com/article/how-to-install-virtualbox-guest-additions-on-a-gui-less-ubuntu-server-host/) & [How to install Virtual Box Guest Additions](https://superuser.com/questions/950431/how-to-install-virtual-box-guest-additions-on-debian)
  - Mount the Guest Additions Image - From the main menu, under _Devices_ choose _Insert Guest Additions CD Image_.
  - Log in as _root_

* In your linux box
  - `mount /dev/dvd` - Should see _WARNING: device write-protected, mounted read only._
  - `apt-get update`
  - `apt-get upgrade`
  - `apt-get install -y dkms build-essential` # Install the necessary dependencies.
  - Install the Guest Additions
    - `cd /media/cdrom`
    - `sh ./VBoxLinuxAdditions.run`
  - Reboot.
  - Login as _root_.
  - Verify that Guest additions were installed. `modinfo vboxguest` - Should see details about the module.
* Install Network Ups Tools. - [Network Ups Tools](https://networkupstools.org)

  - Verify that your UPS is supported - https://networkupstools.org/stable-hcl.html
  - Connect your UPS to your computer using a USB cable.
  - From the Virtual Machine Menu, See if your UPS is listed under _Devices -> USB_
  - Install Network UPS Tools
    - `apt-get install nut`

* Follow the instructions from https://linux-tips.com/t/disabling-ups-beep-under-linux/592 on how to configure and disable the beep from your device.
