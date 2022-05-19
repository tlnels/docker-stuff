# docker-stuff
Here are notes for all my docker learnings and how to configure things with `docker-compose`.

# Nextcloud
Lessons learned:
* Starting a Lets Encrypt container will very your subdomain, you only have five attempts per day at this max before you're locked out. Get it right!

## Issues and Workarounds
1. SVG Support Missing
	* Enter the container with `docker exec CONTAINERID -it /bin/bash` and `apt install libmagickcore-6.q16-6-extra`
2. Mounted volume (block storage) not being chosen
	* Install `local-persist` docker plugin, reference it in the volume config (specified in the current compose manifest already)
3. Default phone region missing
	* Locate the `config.php` file in the actual nextcloud app volume. It'll be in the `data/config` folder and manually add the value to the list of php vars. (TODO Item)

## To Dos
1. Export `default_phone_region` straight into the docker compose rather than editing `config.php` on the app's volume.

# PhpMyAdmin
N/A
