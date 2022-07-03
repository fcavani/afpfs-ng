## Apple Filing Protocol Library - afpfs-ng - libafpclient

### Description

AFPFS is a client implementation of the Apple Filing Protocol written in C which
can be used to access AFP shares exposed by multiple devices, notably Mac OS X
computers, linux devices exporting shares with netatalk, Apple Airport and 
Time Capsule products as well as other NAS devices from various vendors.

This implementation of AFPFS come in hand now when the support for the cifs ntlm version 1.0
was dropped from the linux kernel, what make it a good alternative to access old hardware.

### Installation

Pretty standard unix stuff:
```bash
./configure && make && sudo make install && echo 'done!'
```

Use --disable-fuse and/or --disable-gcrypt if your system cannot meet those dependencies.
(note that disabling gcrypt will prevent you from using login/password auth.)

The command line tool needs ncurses-dev and libreadline-dev to compile. Install them
with sudo apt-get install ncurses-dev libreadline-dev on ubuntu/debian.

### Ubuntu install

Install the following packages on Ubuntu 22.04 system.
```bash
sudo apt-get install g++ libfuse-dev ncurses-dev libreadline-dev libncurses5-dev libgmp3-dev libgcrypt-dev
```

Replace the `configure` command with the bellow (pay attention to the above observation).
```bash
./configure --enable-gcrypt=/usr/lib
```

### Usage

You can either use afpfs to mount an AFP share with fuse or with the command-line client.

#### fuse

Mount the time_travel volume from delorean.local (in this example, my time capsule's hostname)
on /mnt/timetravel without authentication:

```bash
$ mount_afp afp://delorean.local/time_travel /mnt/timetravel
```

Same, with authentication:

```bash
$ mount_afp afp://simon:mypassword@delorean.local/time_travel /mnt/timetravel
```

Same, with authentication, forcing the UAM of your choice (usually not needed):

```bash
$ mount_afp afp://simon;AUTH=DHX2:mypassword@delorean.local/time_travel /mnt/timetravel
```

Unmount the volume:

```bash
$ fusermount -u /mnt/timetravel
```

#### command line client

Open volume time_travel on delorean.local:

```bash
$ afpcmd afp://simon:mypassword@delorean.local/time_travel
```

Connect anonymously to delorean.local, list all available volumes:

```bash
$ afpcmd afp://simon:mypassword@delorean.local/
```

cd to change directories, ls to list, get file to retrieve file, put file to put file...
and help for a list of supported commands.


### Credits and license

This is a fork of the original afpfs-ng project that has gone unmaintained
for quite some time. It is so far the only available open source AFP client.

This repository includes many patches collected by the XBMC project
(www.xbmc.org) as well as mine, in a bid to improve stability, performance and
to implement new features.

Check AUTHORS for a somewhat complete list of contributors.

The original afpfs-ng webiste can be found at https://sites.google.com/site/alexthepuffin/home

This project retains the original author's license and is distributed under the GPL.


### Feedback and patches

Feel free to send your feedback/patches/flames at simon (dot) vetter (at) gmx.com .

