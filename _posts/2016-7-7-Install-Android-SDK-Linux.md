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

To activate this changes just:

```bash
$ source /etc/profile
```

### Install required packages

```bash
$ android list sdk #list packages
$ android update sdk --no-ui --filter *x* #install first package nr. *x*
```

or

```bash
$ android list sdk -all #list all packages
$ android update sdk --no-ui --all --filter *x* #install package nr *x*
```



