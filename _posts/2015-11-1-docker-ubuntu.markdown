---
layout: post
title:  "Friends don't let friends use anything but ubuntu as a docker host"
date:   2015-11-01 00:57:38 +0800
categories: docker
---

Or Why it's important to use ubuntu to host docker in production, and in learning environments.

Simplicity.

We initially went with CentOS, to host our docker containers, that is until it dawned on us that the default docker setup on this OS has a maximum capacity of roughly 107GB. So great for running a few experiments but someday that's going to run out. I also found that for experimenting with docker for more than one purpose was very difficult with such restrictions.

Here's where things became clear. [Friends Don't Let Friends Run Docker on Loopback in Production](http://www.projectatomic.io/blog/2015/06/notes-on-fedora-centos-and-docker-storage-drivers)

There are a few gotchas in docker worth mentioning, such as an internal volume will not be deleted when docker rm is called unless you add the -v flag. Which eats through a lot of space when you are playing around with a db container and not removing the volumes.

Our symptom of an full filesystem was the following error message, mongo spits out when it refuses to start.

{% highlight bash %}
E JOURNAL  [initandlisten] Insufficient free space for journal files
I JOURNAL  [initandlisten] Please make at least 3379MB available in /data/db/journal or use --smallfiles
{% endhighlight %}

Heres the difference between our CentOS and ubuntu found by running the following.
{% highlight bash %}
docker info
{% endhighlight %}

CentOS
{% highlight bash %}
Containers: 6
Images: 80
Storage Driver: devicemapper
 Pool Name: docker-253:0-1049323-pool
 Pool Blocksize: 65.54 kB
 Backing Filesystem: extfs
 Data file: /dev/loop0
 Metadata file: /dev/loop1
 Data Space Used: 4.158 GB
 Data Space Total: 107.4 GB
 Data Space Available: 2.537 GB
 Metadata Space Used: 5.706 MB
 Metadata Space Total: 2.147 GB
 Metadata Space Available: 2.142 GB
 Udev Sync Supported: true
 Deferred Removal Enabled: false
 Data loop file: /var/lib/docker/devicemapper/devicemapper/data
 Metadata loop file: /var/lib/docker/devicemapper/devicemapper/metadata
 Library Version: 1.02.95-RHEL6 (2015-09-08)
Execution Driver: native-0.2
Logging Driver: json-file
Kernel Version: 2.6.32-573.7.1.el6.x86_64
Operating System: <unknown>
CPUs: 4
Total Memory: 15.27 GiB
Name: localhost.localdomain
 {% endhighlight %}
ubuntu
{% highlight bash %}
Containers: 7
Images: 229
Storage Driver: aufs
 Root Dir: /var/lib/docker/aufs
 Backing Filesystem: extfs
 Dirs: 243
 Dirperm1 Supported: true
Execution Driver: native-0.2
Logging Driver: json-file
Kernel Version: 4.2.0-16-generic
Operating System: Ubuntu 15.10
CPUs: 1
Total Memory: 992.9 MiB
Name: ubuntu
 {% endhighlight %}
