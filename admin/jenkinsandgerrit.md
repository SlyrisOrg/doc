### Connecting Jenkins and Gerrit

##### Setup Gerrit for Jenkins
In order to allow Jenkins to look into Gerrit, we need to create a `jenkins` user. This user will need an SSH key, which we will generate as the user running Jenkins:
```bash
jenkins@host> ssh-keygen -t rsa
```

Then we will create the matching account in Gerrit (either using the web UI or the command line), and add it to the 'Non-Interactive Users' group.
We will also create an 'Event Streaming Users' group and add our new user to it.

##### Setup Jenkins for Gerrit
On the Jenkins side, we will need to install the Gerrit trigger plugin. As with other plugins, it can be installed directly from within Jenkins. However, its official documentation is now outdated.

After installing the plugin, we will have to register our Gerrit site in it, which only consists in filling basic information.