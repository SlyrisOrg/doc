### Setting up Gerrit

#### Basic Gerrit install
Gerrit is very easy to install, and has very few dependencies.

We will start by installing a JDK (it contains the JRE required to run Gerrit, and will also allow building plugins if needed).

```bash
gerrit@host> wget https://www.gerritcodereview.com/download/gerrit-2.14.1.war -O gerrit.war
```
<...>

#### OAuth plugin
The default Gerrit uses OpenID to authenticate users. We prefer using OAuth, which allows (amongst others) to login through a Github account.
To achieve that, we need to download, build and install an OAuth plugin for Gerrit.
In order for this documentation to remain as correct as possible over time, we will refer to the official [build instructions](https://github.com/davido/gerrit-oauth-provider).

Once the plugin is built, stop Gerrit and simply drop the generated `.jar` into the `plugins` directory of the review site.
```bash
gerrit@host> ~/reviewsite/bin/gerrit.sh stop
gerrit@host> cp gerrit-oauth-provider.jar reviewsite/plugins/gerrit-oauth-provider.jar
```

Now we need to obtain OAuth tokens for Gerrit. Those need to be obtained from Github's [developer portal](https://github.com/settings/developers), then filled in ```gerrit.config```

```ini
[plugin "gerrit-oauth-provider-github-oauth"]
	client-id = <your-client-id>
	client-secret = <your-client-secret-key>
[oauth]
	allowRegisterNewEmail = true
```

After that, we can change the authentication method to OAuth in that same file and restart Gerrit:
```ini
[auth]
	type = OAUTH
	gitBasicAuthPolicy = HTTP
```

```bash
gerrit@host> ~/reviewsite/bin/gerrit.sh restart
```