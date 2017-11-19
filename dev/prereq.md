### dev/prerequisites

In order to be efficient in our work environment, every developer will need to satisfy a few prerequisites.

##### Account
The first thing you need is an account on each of our developer services.
This can be achieved by logging-in with your GitHub account.

Note that account creation is automatic, however you will need to ask for the appropriate privileges on our Slack channel.

##### Gerrit script
In order to abstract Gerrit's mechanisms away, we use a tiny bash script wrapping the available commands.
It it published on Gist and can be downloaded from [there][0].

It requires a bit of configuration, which can be achieved through the shell environment.
The following definitions should be added to your shell's rc file:

```bash
export GERRIT_HOST=git.slyris.eu
export GERRIT_PORT=29418
export GERRIT_SSHUSER=YourUserName    #the username you use to login into Gerrit, i.e. your GitHub username
```

If your computer-local username is different from your SSH username, an additional step is required since Git otherwise uses SSH with your default username.
You can change that behavior by configuring an SSH alias like below, in the file `~/.ssh/config`:

```
Host git.slyris.eu
     HostName git.slyris.eu
     Port 24198
     User YourUserName
```

##### Code Style settings
Since we mostly use JetBrains IDEs, all developers can easily share the same code style settings.

[Download CLion settings][1]

[0]: https://gist.github.com/doom/ce5a5d51c507a3ffd7fe04f004a03e5f
[1]: http://doc.slyris.eu/resources/clion_code_style.jar
