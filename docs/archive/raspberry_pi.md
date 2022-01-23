# Setting up Raspberry Pi for remote dev
**Version: 20.04.3**
**IP Address: 192.168.100.110**
* Setting up SSH Authentication on my pi server from my mac
	* https://www.digitalocean.com/community/tutorials/how-to-configure-ssh-key-based-authentication-on-a-linux-server
	* https://www.ssh.com/academy/ssh/copy-id
	* `ssh-copy-id -i ~/.ssh/id_rsa ubuntu@192.168.100.110` - from my mac
* Setup zsh as default shell
	* https://www.ubuntupit.com/how-to-install-and-configure-zsh-on-linux-distributions/
```shell
sudo apt update
sudo apt install zsh
sudo chsh -s /bin/zsh ubuntu
```
* Install oh-my-zsh
	* `sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"`
* Install nvm
	* `curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash`
	* `nvm install v17.2.0 --latest-npm --default`
* Add ssh key to github - https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account
* Accounts
	* email: martin.johan@johan-martin.com
	* `ssh-keygen -t ed25519 -C "martin.johan@johan-martin.com"`
	* `cat ~/.ssh/id_ed25519.pub`
* Setup dev environment
	* `sudo apt install build-essential git curl`
## Setup Docker
* https://docs.docker.com/engine/install/ubuntu/
```shell
sudo apt-get update
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```
* Post Install (run docker wihtou sudo)
```shell
sudo groupadd docker
sudo usermod -aG docker $USER
newgrp docker
docker run hello-world
```


## Configure Raspberry
* https://github.com/raspberrypi
* Mirror Website: https://www.raspbian.org/RaspbianMirrors
### Add Raspberry Pi Repositories
* https://www.blackmoreops.com/2021/09/16/add-raspberry-pi-repository-in-ubuntu/
	* `echo deb http://archive.raspberrypi.org/debian/ bullseye main | sudo tee /etc/apt/sources.list.d/raspberrypi.list`
	* `sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 7FA3303E`
* Install `raspi-config`
```shell
sudo apt update
sudo apt install raspi-config
```
### Video
* https://www.raspberrypi.com/documentation/computers/configuration.html#the-kernel-command-line

## Fix issue with Perl Warning about Locale
* https://raspberrypi.stackexchange.com/questions/38019/locale-settings-issues
```shell
sudo nano /etc/default/locale
# LANG=en_US.UTF-8
# LC_ALL=en_US.UTF-8
# LANGUAGE=en_US.UTF-8
```


## Setup Node-RED
* with docker installed
	* docker run -it -p 1880:1880 --name mynodered nodered/node-red
* `bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)`


## Zsh Plugins
* https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/web-search web-search
* https://github.com/zsh-users/zsh-autosuggestions
* https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/sudo
* https://github.com/ohmyzsh/ohmyzsh/tree/master/plugins/jsontools


## PiZeroMonitor
`ssh-copy-id -i ~/.ssh/id_rsa pi@192.168.100.120`
* Turn off display
* `vcgencmd display_power 0`

## Upgrading raspbian from buster to bullseye

* https://www.tomshardware.com/how-to/upgrade-raspberry-pi-os-to-bullseye-from-buster
```shell
sudo apt update
sudo apt dist-upgrade -y
sudo rpi-update
udo nano /etc/apt/sources.list
# Change the line from buster to bullseye and press CTRL + X, then press Y and Enter to save and exit.
sudo apt update
sudo apt dist-upgrade -y
sudo apt autoclean
sudo reboot
```
