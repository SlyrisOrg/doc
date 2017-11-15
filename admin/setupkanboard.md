### Setting up Kanboard

##### Installing Kanboard
Kanboard is quite easy to install, however it depends on a working web server supporting PHP (and a few PHP-related plugins).

For the web server setup, we will refer to our guide about [NGinX](http://doc.slyris.eu/admin/setupnginx.html).

We will start by installing Kanboard's dependencies:
```bash
root@host> apt-get install php7.0-cli php7.0-mbstring php7.0-sqlite3 php7.0-opcache php7.0-json php7.0-mysql php7.0-pgsql php7.0-ldap php7.0-gd
```
Then we will download kanboard from the official website  and proceed with the actual installation:
```bash
root@host> wget https://kanboard.net/kanboard-latest.zip -O kanboard.zip && unzip kanboard.zip
root@host> mv kanboard /var/www/html/kanboard
```

After that, we need to ensure the web server user (usually `www-data` has writing permissions on Kanboard's `data` directory. If that is not the case, we will add them:
```bash
root@host> chown -R www-data /var/www/html/kanboard/data/
```

Kanboard is now properly installed, and will be ready to be used after being enabled in NGinX.

##### Setting up the Nginx site
In order to access our Kanboard site through a subdomain, we will register a site for it within Nginx with the following settings:

```
server {
        listen 80;

        root /var/www/html/kanboard;
        index index.php;

        server_name kbd.slyris.eu;

	location ~ \.php$ {
		 try_files $uri =404;
		 fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
		 fastcgi_index index.php;
		 fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
		 include fastcgi_params;
	}
}
```

##### Installing the GitHub OAuth plugin
In order to login to Kanboard using GitHub accounts, we need to install the GitHub OAuth plugin for Kanboard.

Fortunately, it is an official plugin, and it is well-documented on its [GitHub repository](https://github.com/kanboard/plugin-github-auth).

The only part of its use that might not seem obvious is that unlike most OAuth plugins, it doesn't have the ability to create users.
This means an administrator needs to create Kanboard accounts as external and link them to the users' GitHub IDs manually.