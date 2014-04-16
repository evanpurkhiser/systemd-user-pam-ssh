## Systemd User PAM SSH script

This script has a rather specific use case. If you fit the following demographic
then this script might just be for you!

 * You use systemd
 * You login at the linux VT using a getty
 * You have a `systemd --user` service called `ssh-agent.service` that starts
   your ssh agent.
 * You have to type your password a second time after logging in in order to
   decrypt your SSH key.

This script allows you to only type your password once. When logging in, your
SSH key will be decrypted and added to your ssh-agent for you.

## Usage

There is one pre-requisite for this script:

Your systemd --user instance needs to know about the `SSH_AUTH_SOCK`. If you're
using my systemd-user-sessions package mentioned above then you will want to
add this to your `~/.config/bash/environment` file as something like
`SSH_AUTH_SOCK=$XDG_RUNTIME_DIR/ssh-agent`.

To enable the script you will want to add this to your pam configuration
(probably `/etc/pam.d/system-login` or `/etc/pam.d/login`)

    auth  optional  pam_exec.so  expose_authtok /path/to/the/systemd-user-pam-ssh

## Installation

I would recommend placing the script under `/usr/lib/systemd/`. If you are using
Arch Linux you can use the PKGBUILD [located
here](https://github.com/EvanPurkhiser/PKGBUILDs/tree/master/systemd-user-pam-ssh-git/PKGBUILD).
