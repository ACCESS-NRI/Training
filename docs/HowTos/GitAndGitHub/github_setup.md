# GitHub setup
We present here our recommended setup for GitHub.

## Two-factor authentication

We recommend to [enable 2-factor authentication][2FA] on your GitHub account for higher security. 

## SSH authentification
ACCESS users are used to SSH for connecting to NCI. We recommend setting up [SSH keys][SSHkeys] for pulling from and pushing to GitHub repositories. Remember to set a passphrase for your key, do not use passphrase-less keys.
Use [SSH agent forwarding][SSHagent] to securely forward ssh keys from your own machine to use them on NCI machines.
## Commit signature verification

It is [trivially easy to impersonate another user][Impersonate] when committing to git. This does not lead to elevated privileges, but could be exploited in a social hack, causing commits to be accepted based on an assumption of identity.

Code signing gives others confidence that [code commits come from a trusted source][CommitSign]. Code signing is not required to contribute to ACCESSHub, but it is for contributing to most repositories in the [ACCESS-NRI Organisation][ACCESS-NRI].

GitHub is the code hosting platform used by ACCESS-NRI, and GitHub supports code signing. You know when a commit is correctly signed because the commit has a "Verified" badge:

![PRpreview](../../assets/verified_commit.png)

### Signing code with SSH keys

Code signing with GPG has been supported for some time, but it is somewhat complicated to configure and places a burden to become familiar with and maintain GPG keys.

Since version 2.34.0 git supports code signing with ssh keys. Most people are familiar with using ssh keys for ssh access, which makes configuring code signing more straightforward. 

???+ info
    git 2.37.3 is available as a module on gadi (`module load git/2.37.3`) 
 
First [add your signing key to GitHub][AddKey]. Either use an existing SSH key, or create a new one.

Make sure your key is on your keychain and then login to gadi with key forwarding. 

???+ info
    Adding a key to your ssh agent is platform dependent

    Apple OSX: 

        ssh-add --apple-use-keychain <path to keychain>

    [Linux][LinuxAgent]: 
    
        ssh-add <path to keychain>

To automatically sign *all* commits and tags in *all* repositories with your ssh key:

    git config --global commit.gpgsign true 
    git config --global tag.gpgsign true 

    git config --global gpg.format ssh 
    git config --global user.signingKey <ssh public key signature> 


???+ note
    Ensure you use a modern enough version of git otherwise you will get errors if you try and sign commits 

### Resources

[https://blog.dbrgn.ch/2021/11/16/git-ssh-signatures/](https://blog.dbrgn.ch/2021/11/16/git-ssh-signatures/) 

[https://docs.github.com/en/authentication/managing-commit-signature-verification/telling-git-about-your-signing-key#telling-git-about-your-ssh-key](https://docs.github.com/en/authentication/managing-commit-signature-verification/telling-git-about-your-signing-key#telling-git-about-your-ssh-key) 

[https://calebhearth.com/sign-git-with-ssh](https://calebhearth.com/sign-git-with-ssh) 

[2FA]: https://docs.github.com/en/authentication/securing-your-account-with-two-factor-authentication-2fa/about-two-factor-authentication 
[SSHkeys]: https://docs.github.com/en/authentication/connecting-to-github-with-ssh
[SSHagent]: https://docs.github.com/en/developers/overview/using-ssh-agent-forwarding
[Impersonate]: https://betterprogramming.pub/why-and-how-you-should-sign-all-your-git-commits-94435516edae
[CommitSign]: https://docs.github.com/en/authentication/managing-commit-signature-verification/about-commit-signature-verification
[ACCESS-NRI]: https://github.com/ACCESS-NRI
[AddKey]: https://docs.github.com/en/authentication/managing-commit-signature-verification/about-commit-signature-verification#ssh-commit-signature-verification
[LinuxAgent]: https://wiki.archlinux.org/title/SSH_keys#SSH_agents