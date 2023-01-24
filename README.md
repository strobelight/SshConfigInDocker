# SshConfigInDocker

Many times developers have a `~/.ssh` with a config, and keys, and just want to use it easily within a docker container.

Solutions typically involve creating a special user in the container, and mounting the .ssh directory.

This solution creates a whole new image containing a copy of the .ssh directory, so no mounts or special users are needed.

The downside is, the generated image should **not** be made available for general use (put on a docker hub) since it now contains private keys as well. This may not be so bad if the script is modified to remove them, and startup includes a mounting of the ssh auth socket.

## makewithubuntu
This script builds a ubuntu image with ssh and a copy of your .ssh directory. The .bashrc is modified to start an ssh agent, and add the keys and certs that may be present, prompting for passphrases if needed.
