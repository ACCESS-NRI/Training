# Git setup

Make sure you set up git on every machine (including servers such as HPCs for example) you work on.

## Config name and email

All commits on git have information about the author with the name and email address. Before any work with Git, you should configure them globally for each machine you use by typing in a terminal:

```
$ git config --global user.email "YOUR_EMAIL"
$ git config --global user.name "YOUR_NAME"
```

## Config auto-remote

When working collaboratively with git, you will need to synchronise your work between your local work area and a remote repository. To remove the need to manually set up the remote connection for each branch, you can set this configuration option:

```
$ git config --global --add push.autoSetupRemote true
```