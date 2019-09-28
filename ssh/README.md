config - SSH Hosts
===============

This guide is meant to help students set up SSH hosts on their system. It enables aliases like `student.cs` to replace `username@linux.student.cs.uwaterloo.ca`, and allows users to access remote servers through a jump host.

1. [Jump Hosts](#jump-hosts)
1. [Setup](#setup)

# Jump Hosts
Some servers are protected by a security zone. This means they cannot be accessed from outside a private network. Normally, one would access the server by connecting to the same Wi-Fi network as the server, using a VPN, or SSHing to a machine that has access to the network. At UWaterloo, the Ugster server is protected by the campus security zone. The easiest way to gain access to this server is by SSHing to the `student.cs` environment and then SSHing to the Ugster environment. A jump host does exactly this, except it removes the need to SSH twice. Instead, it uses the `student.cs` server as a "jump host" to jump to Ugster. The end result is you only need to type `ssh ugster` to access the Ugster environment!

# Setup
Navigate to `~/.ssh`, creating the directory if necessary. Open / create a `config` file inside. Copy the following 2 entries into `config`, replacing `<username>` with your UWaterloo username. If you do not have an Ugster account, you may delete the second entry. The second entry is an example of how to utilize `student.cs` as a jump host. Note that in Windows, you will need to replace `ProxyCommand ssh` with `ProxyCommand C:\Windows\System32\OpenSSH\ssh.exe` due to a bug with OpenSSH.

```
Host student.cs
  User <username>
  Hostname linux.student.cs.uwaterloo.ca

Host ugster
  User <username>
  Hostname ugster<##>.student.cs.uwaterloo.ca
  ProxyCommand ssh -q -W %h:%p student.cs
```

After you have saved the `config` file, you should be able to use `ssh student.cs` and `ssh ugster` to connect to the servers. To use SSH key authentication on Ugster environment, you will need to copy the public key from **your local machine** to the Ugster environment's `authorized_keys` file.

If you have set up the [uw script](https://github.com/george-lim/uwaterloo-script-archive/tree/master/uw) as well, you may replace the value of `UW_SERVER` inside `uw` with `student.cs` since they represent the same host.