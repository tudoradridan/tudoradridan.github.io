---
layout: post
title: Install Android SDK on Linux
---

After struggling to install Android SDK, let me share with you my experience.

### Download SDK and unpack

```bash
$ cd /opt
$ wget https://dl.google.com/android/android-sdk_r24.4.1-linux.tgz
$ tar -xzvf android-sdk_r24.4.1-linux.tgz
```

### Add ANDROID_HOME and change PATH

```bash
$ vim /etc/profile.d/android
```

Add the following lines:

```text
export ANDROID_HOME="/opt/android-sdk-linux"
export PATH="$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools:$PATH"
```

To activate this changes without restart just:

```bash
$ source /etc/profile
```

### Install required packages

#### Very imprortant here!

`--all` parameter is important if you want to install older packages. If you use it with the `android list` command, you **must** use it with `android update sdk` command also. Otherwise the package number from `filter` parameter will get you a different package.

```bash
$ android list sdk #list packages
$ android update sdk --no-ui --filter x #install package nr. x
```

or

```bash
$ android list sdk --all #list all packages
$ android update sdk --no-ui --all --filter x #install package nr x
```

Good luck!

