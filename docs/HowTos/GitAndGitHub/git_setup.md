# Git setup

Git has many configuration options. This section covers some of the basic options that are recommended. 
Make sure you set these configuration options on every machine you routinely use, including remote servers such as HPCs.

## Configure name and email

All commits on git have information about the author with the name and email address. Before any work with Git, you should configure them globally for each machine you use. See [the GitHub documentation][git-setup] to guide you through it.

## Configure auto-remote

When working collaboratively with git, you will need to synchronise your work between your local work area and a remote repository. To remove the need to manually set up the remote connection for each branch, you can set this configuration option:

```bash
$ git config --global --add push.autoSetupRemote true
```

[git-setup]: https://docs.github.com/en/get-started/quickstart/set-up-git#setting-up-git