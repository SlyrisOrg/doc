### Setting up Jenkins

##### Installing Jenkins
For Debian users, Jenkins can be installed through `apt-get`.

We'll start by adding Jenkins' repository to APT:
```bash
root@host> wget -q -O - https://pkg.jenkins.io/debian/jenkins-ci.org.key | sudo apt-key add -
root@host> echo deb http://pkg.jenkins.io/debian-stable binary/ | tee /etc/apt/sources.list.d/jenkins.list
```
Then we can install the `jenkins` package and run it as a service:
```bash
root@host> apt-get update && apt-get install jenkins
root@host> service jenkins start
```

Jenkins is now running on port `8080` and can be accessed through a web browser to finish the setup.

##### Installing the OAuth plugin
The default Jenkins uses its own way to authenticate users. We prefer using OAuth, which allows (amongst others) to login through a Github account.
To achieve that, we need to and install an OAuth plugin for Jenkins.

The plugin can be installed from within Jenkins, and its setup is explained [here](https://wiki.jenkins.io/display/JENKINS/GitHub+OAuth+Plugin).


##### Setup the Nginx site
In order to access our Jenkins site through a subdomain, we will create a site for it in Nginx with the following settings:

```
server {
       listen 80;

       server_name ci.domain.com;

       location / {
                proxy_pass http://localhost:8080;
       }
}
```