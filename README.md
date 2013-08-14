## Systemd User SSH PAM

This script has a rather specific use case. If you fit the following demographic
then this script might just be for you!

 * You use systemd as a user session manager (either
   [this](https://github.com/sofar/user-session-units), or [this](https://github.com/EvanPurkhiser/systemd-user-sessions)
 * You have a `systemd --user` service called `ssh-agent.service` that starts
   your ssh agent.
 * You hav to type your password a second time after logging in in order to
   decrypt your SSH key.

This script lets you only type your password one, both logging you in and
decrypting your ssh key and adding it to your agent.

## Usage

There are a few pre-requisits to this script:

 1. Your systemd --user session needs to be started during login time. This wont
    be a problem if you use one of the user-session services mentioned above.
 2. Your systemd --user instance needs to know about the SSH_AUTH_SOCK. If
    you're using my systemd-user-sessions package mentioned abouve then you will
    want to add this to your `~/.config/bash/environment` file as something like
    `SSH_AUTH_SOCK=$XDG_RUNTIME_DIR/ssh-agent`

To enable the script you will want to add this to your pam configuration
(probably `/etc/pam.d/system-login` or `/etc/pam.d/login`

    auth  optional  pam_exec.so  expose_authtok /path/to/the/systemd-user-pam-ssh

## Installation

I would recomend placing the script under `/usr/lib/systemd/`. If you are using
Arch Linux you can use the PKGBUILD [located
here](https://github.com/EvanPurkhiser/PKGBUILDs/tree/master/systemd-user-pam-ssh-git/PKGBUILD)
