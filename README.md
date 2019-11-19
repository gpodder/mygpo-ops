# mygpo-ops
operations of gpodder.net


## Configuration

The `conf` directory of this repository conatins the relevant configuration to run gpodder.net.


### mygpo

[mygpo](https://github.com/gpodder/mygpo) is the source code for gpodder.net.
All files should be placed in `/srv/mygpo/envs/prod`. See the [Configuration
documentation](https://gpoddernet.readthedocs.io/en/latest/dev/configuration.html)
for the purpose of the individual settings.

The following config values are secrets and therefor **not** stored in this repository:
* DATABASE_URL
* FLATTR_SECRET
* FLICKR_API_KEY
* GOOGLE_CLIENT_SECRET
* OPBEAT_SECRET_TOKEN
* SECRET_KEY
* SENTRY_DSN
* SOUNDCLOUD_CONSUMER_KEY
* STAFF_TOKEN


### letsencrypt

gpodder.net uses certificates by [Let's Encrypt](https://letsencrypt.org/).

| Filename          | Location                  | Purpose                                  |
| ----------------- | ------------------------- | ---------------------------------------- |
| gpodder.net.conf  | /etc/letsencrypt/renewal/ | certbot config for renewing certificates |
| letsencrypt-renew | /etc/cron.daily/          | Cron-Job to renew certificates           |


### nginx

gpodder.net uses [nginx](https://nginx.org/) as a reverse proxy.

| Filename        | Location                  | Purpose                                                                    |
| --------------- | ------------------------- | -------------------------------------------------------------------------- |
| feedservice     | /etc/nginx/sites-enabled/ | Could be used to run feeds.gpodder.net locally; currently hosted on Heroku |
| gpodder         | /etc/nginx/sites-enabled/ | Plain HTTP config file for gpodder.net; redirects most to HTTPS            |
| gpodderorg.conf | /etc/nginx/sites-enabled/ | Hosts gpodder.org; mostly redirecting to other services                    |
| gpodder-other   | /etc/nginx/sites-enabled/ | Serves gpodder.net on other hostnames (eg old my.gpodder.org)              |
| gpodder-ssl     | /etc/nginx/sites-enabled/ | Main HTTPS reverse proxy file for gpodder.net                              |
| nginx.conf      | /etc/nginx/               | main nginx config file which loads the other files                         |


### postfix

gpodder.net uses [postfix](http://www.postfix.org/) for sending mails.

| Filename | Location      | Purpose                  |
| -------- | ------------- | ------------------------ |
| main.cf  | /etc/postfix/ | main postfix config file |


### supervisord

gpodder.net uses [supervisord](http://supervisord.org/) to keep its different mygpo services up and running.

| Filename   | Location                | Purpose                    |
| ---------- | ----------------------- | -------------------------- |
| mygpo.conf | /etc/supervisor/conf.d/ | defines the mygpo services |
