# Mongo DB with MacPorts
## Resources
* [Mongo Site](https://docs.mongodb.com/)
## Setup
* `sudo port install mongodb mongo-tools`
* Setup configuration
    * */opt/local/etc/mongodb.conf*
```ini
dbpath = /opt/local/var/db/mongodb

bind_ip = 127.0.0.1

# Running as daemon
fork = true

logpath = /opt/local/var/log/mongodb/mongodb.log
logappend = true
```
* Configure ~/.profile
```bash
alias mongostart="sudo mongod -f /opt/local/etc/mongodb/mongod.conf --httpinterface"

mongostop_func () {
	local mongopid = `less /opt/local/var/db/mongodb/mongod.lock`;
	if [[ $mongopid =~ [[:digit:]] ]]; then
		sudo kill -15 $mongopid;
		echo mongod process $mongopid terminated;
	else
		echo mongo process $mongopid not exists;
	fi
}

alias mongostop="mongostop_func"
```
* Start the server
    * `mongostart` - will need sudo password
