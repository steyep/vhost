## vhost
This script is for updating all of the files associated with adding a new local development site. Running, `sudo vhost add` will add the new host (defaults to the name of your current directory) to `/private/etc/hosts`, generate ssl cert/keys for the host, configure the `httpd-vhosts.conf` file, and restart Apache. Because of this, it must execute as `root`.

### Installation:
* With [Homebrew](http://brew.sh)
	
	```
	brew tap steyep/tap
	brew install vhost
	```

* Cloning from source:
	
	```
	git clone git@github.com:steyep/vhost.git && cd ./vhost/
	chmod +x vhost
	sudo ln -sv $PWD/vhost /usr/bin/vhost
	```

### Before you get started:
* It's not a bad idea to make a back up of the files that will be modified by this script:
	* `cp /private/etc/hosts ~/hosts.backup`
* This script is specific to my local develoment environment so it may need to be tweaked to fit your needs. Check out the [brewStack docs](https://gist.github.com/steyep/431777908be1fc9b2198) for more information. 

### Configuration
* The first time you run `vhost`, a config file will be generated with several default values. The values should work for most development setups using the native Apache installation. Tweak to your liking. 
* You can access and edit the configuration at anytime:
	* `sudo vhost config`

### Example:
* Add example site:

	```
	mkdir -pv ~/Desktop/vhost-example/mytestsite
	echo '<?php phpinfo();' > ~/Desktop/vhost-example/mytestsite/index.php
	sudo vhost add --path ~/Desktop/vhost-example/mytestsite --host site1 --ssl false
	open http://site1.dev/
	```

* Add SSL example site:
	
	```
	mkdir -pv ~/Desktop/vhost-example/myssl-site
	cd $_
	echo '<?php phpinfo();' > ./index.php
	sudo vhost add --ssl true
	open https://myssl-site.dev/
	open http://myssl-site.dev/
	```

* Remove example sites: 

	```
	sudo vhost rm --host site1
	sudo vhost rm --host myssl-site
	```