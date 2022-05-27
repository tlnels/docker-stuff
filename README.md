# docker-stuff
Here are notes for all my docker learnings and how to configure things with `docker-compose`.

# Initial Setup
1. Create the following externally accessible networks:
	* `backend`
	* `nextcloud`
	* `traefik`

# Nextcloud
Lessons learned:
* Starting a Lets Encrypt container will very your subdomain, you only have five attempts per day at this max before you're locked out. Get it right!

# Wordpress
Lessons learned:
* For small sites, probably its just easiest to load the database and data files right in the compose directory. The `.gitignore` has been updated to ignore these folders based on my conventions.
* My blog is small enough that reinstalling into a new database and importing the post XML was easier than restoring from DB which seemed to fail because of the lack of dockerization and missing files.

## Issues and Workarounds
1. SVG Support Missing
	* Enter the container with `docker exec -it CONTAINERID /bin/bash` and `apt install libmagickcore-6.q16-6-extra`
2. Mounted volume (block storage) not being chosen
	* Install `local-persist` docker plugin, reference it in the volume config (specified in the current compose manifest already)
3. Default phone region missing
	* Locate the `config.php` file in the actual nextcloud app volume. It'll be in the `data/config` folder and manually add the value to the list of php vars. (TODO Item)
4. Might not be an issue but now that I am using `traefik` as a reverse proxy, we might need to start over on Let's Encrypt stuff.

## To Dos
1. Export `default_phone_region` straight into the docker compose rather than editing `config.php` on the app's volume.
2. Learn docker secrets, so I can commit `.env` files to the repo without sharing sensitive credentials.

# PhpMyAdmin
Lessons learned:
* Database containers should really be 1:1 to apps, therefore its useful to create external `networks` for the apps you want to look at in PhpMyAdmin. After these networks exist externally, then you can add the relevant networks to the `docker-compose.yml` of this app (already done, for today's apps).

# Wireguard
Trivial configuration with image, just see the [external documentation](https://github.com/linuxserver/docker-wireguard) and [this guide](https://www.the-digital-life.com/wireguard-docker/).
