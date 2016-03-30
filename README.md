## vhost
This script is for updating all of the files associated with adding a new local development site. Running, `sudo vhost add` will add the new host (defaults to the name of your current directory) to `/private/etc/hosts`, generate ssl cert/keys for the host, configure the `httpd-vhosts.conf` file, and restart Apache.

### Installation:
1. `git clone git@github.com:steyep/vhost.git && cd ./vhost/`
2. `chmod +x vhost`
3. `sudo ln -sv $PWD/vhost /usr/bin/vhost`

### Before you get started:
* It's not a bad idea to make a back up of the files that will be modified by this script:
	* `cp /private/etc/hosts ~/hosts.backup`
* This script is specific to my local develoment environment so it may need to be tweaked to fit your needs. Check out the [brewStack docs](https://gist.github.com/steyep/431777908be1fc9b2198) for more information. 

### Example:
* Add example site:

	```
	cd example/
	sudo vhost add
	open https://example.ste
	```

* Remove example site: 

	```
	# Path to site directory and Host name can also be passed in as options:
	cd ~/Desktop
	sudo vhost rm --path "$(dirname $(readlink /usr/bin/vhost))/example" --host "example"
	```