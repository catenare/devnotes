# Setup Virtualbox with Apline Linux
## Resources
* [Alpine Linux](https://www.alpinelinux.org)
* Docker Alpine Config [fguillot/docker-alpine-nginx-php7](https://github.com/fguillot/docker-alpine-nginx-php7/blob/master/Dockerfile)
* [Vagrant Instructions](https://www.vagrantup.com/docs/boxes/base.html)
* [Packaging the Box](https://www.vagrantup.com/docs/virtualbox/boxes.html)
* [Setting up a ssh-server](https://wiki.alpinelinux.org/wiki/Setting_up_a_ssh-server)
* [AlpineLinux VM under VirtualBox](http://mowson.org/karl/2016/2016-05-20_alpinelinux_vm_under_virtualbox/)

## Host Machine
* Install alpine plugin - `vagrant plugin install vagrant-alpine`

## Instructions
### Download Alpine Linux distribution and install in VirtualBox
* [Alpine Linux Downloads](https://www.alpinelinux.org/downloads/) - Download Virtual Distribution for x86_64.
* [VirtualBox Install](https://wiki.alpinelinux.org/wiki/Install_Alpine_on_VirtualBox)
  * 1GB Ram, 8GB HD
* Install Alpine Linux
  * Mount *alpine-virt-3.6.1-x86_64.iso* to start installation
  * Login with *root*
  * `setup-alpine` to install
  * `poweroff` to turn off the virtualbox
  * Remove virtual iso
* Setup Alpine box
  * Uncomment extra repositories
    * `vi /etc/apk/repositories`
  * `apk update` - get latest package list
  * `apk upgrade` - Upgrade to latest versions
  * `apk add bash` - Install base
  * `apk add sudo` - Add sudo
  * `adduser vagrant` - vagrant user
  * ~~`vi /etc/sudoers`~~
  * Use **visudo**
    * Add line: `vagrant ALL=(ALL) NOPASSWD: ALL` - add sudo without password
* Edit */etc/ssh/sshd_config
    * set **UseDNS no**
* Setup Virtualbox
  * [VirtualBox guest additions](https://wiki.alpinelinux.org/wiki/VirtualBox_guest_additions)
    * `echo "http://nl.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories`
    * `apk add virtualbox-additions-grsec`
    * ~~`apk add virtualbox-guest-additions-5.1.22-r2`~~
    * ~~`echo vboxpci >> /etc/modules`~~
    * ~~`echo vboxdrv >> /etc/modules`~~
    * ~~`echo vboxnetflt >> /etc/modules`~~
  * `reboot`

### Setup Vagrant
* Create Vagrant base
    * `vagrant package --base {virtualbox}`
    * `vagrant box add alpine-linux package.box`
    * `vagrant init alpine-linux`
    *  Install vagrant plugin for alpine - `vagrant plugin install vagrant-alpine`
    *  Configure Vagrantfile [maier/packer-templates](https://github.com/maier/packer-templates/blob/master/alpine3.6/Vagrantfile)
```ruby
    Vagrant.configure(2) do |config|
    config.vm.define 'alpine' do |alpine|
        alpine.vm.box = 'maier/alpine-3.6-x86_64'
        # alpine.ssh.username = 'vagrant'
        # alpine.ssh.password = 'vagrant'

        # NOTE:
        # 	there are *no* guest additions installed
        # 	for alpine linux - the guest additions
        # 	installer fails. once workarounds are
        # 	identified the vbga will be added
        # 	to the base box.
        #
        # since there are no vbga. if the vagrant-alpine plugin
        # is installed it can at least configure the system to
        # enable shared folders.
        #
        alpine.vm.synced_folder '.', '/vagrant', disabled: true
        #
        # after `vagrant plugin install vagrant-alpine`
        # comment the disabled synced_folder line above and
        # uncomment the following two lines
        #
        # alpine.vm.network 'private_network', ip: '192.168.100.10'
        # alpine.vm.synced_folder '.', '/vagrant', type: 'nfs'

        alpine.vm.provider 'virtualbox' do |vb|
            # vb.gui = true
            vb.name = 'Alpine'
            vb.cpus = 1
            vb.memory = 1024
            vb.customize [
                'modifyvm', :id,
                '--natdnshostresolver1', 'on',
                '--nic1', 'nat',
                '--cableconnected1', 'on'
            ]
        end
    end
end
```
    * `vagrant up`

### Install packages
```
apk update && \
apk add nginx bash ca-certificates s6 curl ssmtp php7 php7-phar php7-curl \
php7-fpm php7-json php7-zlib php7-xml php7-dom php7-ctype php7-opcache php7-zip php7-iconv \
php7-pdo php7-pdo_mysql php7-pdo_sqlite php7-pdo_pgsql php7-mbstring php7-session \
php7-gd php7-mcrypt php7-openssl php7-sockets php7-posix php7-ldap php7-simplexml
```
## Other Notes
### Misc
* Search for packages - `apk search {name}`
### Shutdown
* `poweroff`
* `halt`
### Accessing services on the guest box
* Setup Port Forwarding
  * ssh - local port 2222 - guest host port - 22
  * Use `ssh -p 2222 vagrant@127.0.0.1` - will give you access to the guest box

# Docker Base Alpine Image
## Use a base alpine image for docker
* [Official Alpine Docker Image](https://hub.docker.com/_/alpine/)
* [Docker Store](https://store.docker.com/images/alpine)
  * `docker pull alpine`
  * `apk --no-cache add {package}`
  * Dockerfile Example - avoids using *--update* and *rm -rf /var/cache/apk/\**
```yaml
  FROM alpine:latest
  RUN apk add --no-cache nginx
  EXPOSE 80
  CMD ["nginx", "-g", "daemon off;"]
```