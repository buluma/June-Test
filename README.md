Firefox Tweet Machine
=====================

## Requirements

- PHP 5.2 ( with: php-curl, [memcache](http://pecl.php.net/package/memcache) )
- Memcached
- The app must be able to write to a ftm_config.yml in the app root dir

## Setup

> Setup is pretty straightforward, just download and extract the tarball from github to the web root dir.

**Twitter OAuth**

> The management interface uses twitter oauth for authentication, currently the oauth consumer key and secret for the twitter application are set in lib/twitteroauth/secret.php, **they'll have to be reset and removed from the repo before going into production.** (also as a note: oauth callbacks will have to be changed to the final domain)

> Upon first login a config file (ftm_config.yml) will be created in the root directory (the included .htaccess denies access to it) and assign the current twitter username to the allowed admins. It is up to that user to add more usernames to the comma allowed admins separated list in the management interface.

**ftm_config.yml**

> Every configuration field, except allowed admins and whitelisted username, has a hard coded default value,
so the app should be up and running right after deployment unless the default values aren't appropriate
ex: memcache host/port (localhost:11211)

**set up cron job**

>    /usr/bin/php $WEB_TOOT/cron.php >/dev/null 2>&1

> remember to add the memcache.so extension to you cli php.ini

**minimize javascript**

    cd assets/js ; \
    rm minimized.js ; \
    java -jar ../misc/compiler.jar \
    --js=jquery-1.5.2.min.js \
    --js=box2d-min.js \
    --js=preloadCssImages.jQuery_v5.js \
    --js=jquery.timeago.js \
    --js=raphael-min.js \
    --js=jquery.colorbox-min.js \
    --js=jquery.history.js \
    --js=global.js \
    --js=gauge.js \
    --js=keyboard.js \
    --js=preload.js \
    --js=webtrends.js \
    --js_output_file=minimized.js