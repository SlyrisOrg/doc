### How to Git

This page could go on for hours about Git, but it would be quite useless since the Internet already contains a bunch of good tutorials about it.

##### How does it work ?
[This article](https://www.miximum.fr/blog/enfin-comprendre-git/) is a good introduction to Git, and yet it gives a clear overview of how it works.

##### When to commit ?
When developing, we will split the work into features, which will be tied to a commit.

Since we use Gerrit for code review, we can consider commits as pull requests on a public repository (see [the Gerrit tutorial](http://doc.slyris.eu/dev/howtogerrit.html "Gerrit basics and rules") for details).

We'll try to keep a few rules when it comes to committing:

* A commit should only contain one feature
* The feature must be completed and tested before committing
* Don't commit tiny fixes along with another feature ! Make separate commits

##### How to commit ?
The most important moment of a Git-based workflow is committing, and among the most important parts of a commit is its message. [This post](https://chris.beams.io/posts/git-commit/) discusses that topic in detail and gives a well-thought standard, which we'll use.