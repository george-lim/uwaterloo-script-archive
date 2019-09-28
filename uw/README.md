uw - Linux Environment Mounting & SSH Script
===============

This guide is meant to help students set up a better Linux environment. It is written under the assumption that your system is running macOS.

1. [Benefits](#benefits)
1. [Configuring uw](#configuring-uw)
1. [Installing SSHFS](#installing-sshfs)
1. [Configuring SSHFS Flags](#configuring-sshfs-flags)
1. [Mount/SSH Without Password](#mountssh-without-password)

# Benefits
* No need to remember your SSH server.
* Edit files from the Linux environment on your machine, using your favourite IDE/text editor. No need to SCP files between environments!

# Configuring uw
Firstly, `chmod 755 uw` to give `uw` executable permissions. If you want to call `uw` from any directory, add `alias 'uw'='<uw_path>'` to your `~/.bash_profile`.
Now open `uw` in a text editor. In the `Configuration.` section, replace `<USERNAME>` with your Quest username (eg. l69ol). Modify `UW_MOUNT_DIR` to change where the Linux environment is mounted. The default location is set to `Desktop/UWaterloo`.
We still need to figure out the path of `UW_HOME`, which is specific to each person. First SSH into your Linux environment with `uw ssh`. After you are logged in, call `pwd` in the Linux environment. Save the output of `pwd` as the value of `UW_HOME`. You have now finished configuring the `uw` script.

# Installing SSHFS
To mount the Linux environment onto your computer, you will need to download and install SSHFS. Follow [this guide](https://www.digitalocean.com/community/tutorials/how-to-use-sshfs-to-mount-remote-file-systems-over-ssh) to set up SSHFS. Once you are done, call `uw mount` and check your `UW_MOUNT_DIR` directory for the Linux environment. To unmount the Linux environment, call `uw umount`.

# Configuring SSHFS Flags
**(OPTIONAL)** By default, SSHFS is configured with various flags like `volname=UWaterloo` to set the mounted volume name. SSHFS is also currently set to `reconnect` to the Linux environment after it fails to connect `ServerAliveCountMax` times in a row. SSHFS will check for connection every `ServerAliveInterval` seconds.

# Mount/SSH Without Password
Follow [this guide](https://uwaterloo.ca/math-faculty-computing-facility/creating-ssh-keys) to create and upload your public SSH key to the Linux environment for authentication.
