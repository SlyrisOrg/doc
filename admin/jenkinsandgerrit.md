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

After installing the plugin, we will have to register our review site in it, which only consists in filling basic information about the server hosting Gerrit. We will use the `jenkins` account and the previously-generated SSH key to identify ourselves.


##### Creating a Jenkins job to watch on a Gerrit repository
Once everything is setup, we can start creating our automated jobs.
To create a job triggered by Gerrit events, we start by creating a **Freestyle Project** in Jenkins.

Under **Source Code Management**, we will select Git, and fill the following information in the Repositories tab:
- URL: `ssh://jenkins@your.gerrit.host:port/project_name`
- Credentials: select the credentials you previously configured
- Refspec: `$GERRIT_REFSPEC`

Then we the branch specifier to `$GERRIT_BRANCH`, and add an additional behavior in the corresponding tab.
As a strategy, we will choose `Gerrit Trigger`.

Under **Build Trigger**, we will obviously select `Gerrit Event`, and proceed on filling the required information.
Most parts are well explained by Jenkins. For the **Gerrit Project** part, select `Plain` and type in the project name in the **Pattern** tab.
For the branches, select `Path` and type `**` to select all the branches, or customize it to pick only matching branches.

After that, we can freely add build steps to our newly created job.