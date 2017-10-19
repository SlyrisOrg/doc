### Setting up NGinX

##### Installing NGinX
Installing NGinX is trivial since it is available as a package on the default APT repositories.

```bash
root@host> apt-get install nginx
```

##### Creating a site
NGinX works with "server blocks" or "sites", which act like dedicated hosts.
These can be defined through configuration files that are to be placed inside the `/etc/nginx/sites-available` directory.

To enable a site, create a symlink in `/etc/nginx/sites-enabled` pointing at the original configuration file.

##### Restarting NGinX
When modifying its configuration, NGinX can require to be restarted.

```bash
root@host> service nginx restart
```