### How to Gerrit
Gerrit is a tool that works on top of Git and manages code reviews and branches.

The great thing about it is that it eliminates time-consuming things from our Git workflow: creating temporary branches for reviews, merging them, or deleting them.

##### Commits
Gerrit handles commits in a way that reminds **pull requests**. It creates a patchset with the content of the commit, stores it on a hidden branch, and sets up a web page so it can be reviewed.

When the commit is accepted, Gerrit can merge it on the `master` branch for us in a simple click.

##### Drafts
When a feature is in progress, but you still need a feedback, or you want to run tests, etc, use a **draft**.
A draft is a hidden commit which can only be seen by its author and assigned reviewers.
If considered appropriate, drafts can be promoted to regular commits and submitted to global review.

##### How to commit using Gerrit ?
From a developer point of view, it mostly goes through Git transparently.

However, some commands, like cloning, pushing or drafting need a bit of wrapping, which is why we provide a `gerrit` command to help dealing with them.

Here is a tiny summary of common commands:


|          Action           |             Command to use           |
|---------------------------|--------------------------------------|
|          Cloning          | `user@host> gerrit clone <projname>` |
|         Committing        | `user@host> git commit`              |
| Modifying a patch / draft | `user@host> git commit --amend`      |
|    Pushing a new patch    | `user@host> gerrit push`             |
|    Pushing a new draft    | `user@host> gerrit draft`            |


All the rest can be done using the plain old Git commands.