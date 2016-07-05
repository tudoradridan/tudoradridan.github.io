---
layout: post
title: Connect to remote GIT using SSH from Android Studio (Windows)
---
Android Studio won't let you connect to remote SSH Git repository with user and password, so we need to use asymmetric cryptography.

# Create a pair of RSA keys

The pair of keys can be create anywhere, on any server, on any account. The public key will stay on the GIT server, and the private key on our machine.

This command generates a set of keys, default names are **id_rsa** for the private key and **id_rsa.pub** for the public key.

```sh
$ ssh-keygen -t rsa
```

# Place the keys where they belong

## Server

Let's assume we'he created the set of keys on the Git server machine. Next copy the public key **id_rsa.pub** into authorized_keys file in the **.ssh** directory of user home directory:

```sh
$ cat [path]/id_rsa.pub >> /home/[user]/.ssh/authorized_keys
```

## Configure ssh client on Windows
Copy the private key **id_rsa** on your windows machine using WinSCP.
Create a file name config and place it under .ssh directory. Ex. C:\Users\\[your username]\\.ssh\config

Edit the like this:

```txt
Host    [server url or IP]
        HostName        [server url or IP]
	Port            22
	IdentityFile    C:\Users\[your username]\.ssh\id_rsa
```

Now you can commit and push from Android Studio.
