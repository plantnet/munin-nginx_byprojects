# munin-nginx_byprojects

Munin plugin to graph nginx requests per second, per vHost.

Can graph multiple vHost traffic data on a single chart.

## description

This is a fork of the `byprojects_access` script of [nginx_byprojects](https://github.com/munin-monitoring/contrib/blob/master/plugins/nginx/nginx_byprojects/byprojects_access) by Danny Fullerton, see [original license file](https://github.com/munin-monitoring/contrib/blob/master/plugins/nginx/nginx_byprojects/LICENSE.txt)

Licensed under GPLv2 for compliance with https://github.com/munin-monitoring/contrib repo license

## requirements

`logtail`

`perl`

`libjson-perl`

## install
copy `byprojects_access` to whatever place, for ex. `/usr/local/munin/plugins/`
```sh
mkdir -p /usr/local/munin/plugins/
cp byprojects_access /usr/local/munin/plugins/
```

make it executable:
```sh
chmod a+x /usr/local/munin/plugins/byprojects_access
```

create symlinks in `/etc/munin/plugins/` for each graph you wish to draw, one graph allowing multiple vHosts, for ex.
```sh
ln -s /usr/local/munin/plugins/byprojects_access /etc/munin/plugins/byprojects_prod
ln -s /usr/local/munin/plugins/byprojects_access /etc/munin/plugins/byprojects_test
```
(see "configuration" below)

## configuration
copy `byprojects_access.conf.example` to `/etc/munin/plugin-conf.d/`
```sh
cp byprojects_access.conf.example /etc/munin/plugin-conf.d/byprojects_access
```

edit `/etc/munin/plugin-conf.d/byprojects_access`:
 * add a `[byprojects_XXXX]` section for each graph 
 * add an `env.site.*` entry for each vHost and set the actual path(s) to the vHost log(s)
 * add a `group` directive with a group that has read access to nginx logs
 * add a custom `graph_title` directive for each graph

restart `munin-node`
```sh
systemctl restart munin-node
```
