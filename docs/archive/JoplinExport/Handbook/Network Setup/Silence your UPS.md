---
title: Silence your UPS
updated: 2021-04-08 02:58:43Z
created: 2020-01-11 07:12:57Z
---

# Silence your UPS - 
* Now using a Raspberry PI Zero
* `ssh pi@192.168.100.100`
## Disable the beep 
```
upscmd myups@localhost beeper.disable
Username: admin
Pasword: pass
```
## Setup
### Check that UPS is visible via UPS
### Install the Network UPS Tools - [Network Ups Tools](https://networkupstools.org)
* Verify that your UPS is supported - https://networkupstools.org/stable-hcl.html
* Connect your UPS to your computer using a USB cable.
* From the Virtual Machine Menu, See if your UPS is listed under Devices -> USB
/Capture USB.png
* `apt-get install nut` - install nut.
#### Configure Network UPS Tools
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

	