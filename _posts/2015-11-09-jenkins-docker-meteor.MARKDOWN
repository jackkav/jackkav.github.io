---
layout: post
title:  "Jenkins Docker Meteor"
date:   2015-11-09 00:57:38 +0800
categories: jenkins docker
---
# How to set up you own simple Jenkins CI inside a container to build meteor a meteor project from a git url and push it to a folder somewhere.

This build assumes you have already got meteor running using the meteorhacks/meteord:base image, which by default will grab your meteor bundle from the directory at: ~/app


##Create jenkins container

{% highlight bash %}
docker run -d --name jenkinsci --restart=always -p 8080:8080 -p 50000:50000 -v /var/jenkins_home jenkins
{% endhighlight %}

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}


Point your browser at your docker url:8080, Go to Manage Jenkins, Manage Plugins, install git plugin.

##Install meteor on the jenkins server

{% highlight bash %}
docker exec -it jenkinsci /bin/bash
curl https://install.meteor.com/ | sh
export PATH=$PATH:$HOME/.meteor
ssh-keygen
#=>Don't use a password
ssh-copy-id MYUSER@172.17.42.1
#=>This ip is the default docker host IP
{% endhighlight %}


##Set up a jenkins task with your git address, set poll SCM to every 5 minutes and bash script as follows:

    H/5 * * * *


{% highlight bash %}
meteor build --architecture=os.linux.x86_64 ./
scp *.tar.gz MYUSER@172.17.42.1:~/app/MYMETEORAPP.tar.gz
ssh MYUSER@172.17.42.1 ‘docker restart MYMETEORCONTAINER && exit’
{% endhighlight %}




Next steps:

Use jenkins slave agents, instead of running the build on jenkins host would allow multiple deploy targets.

Making jenkins accessible to the web would allow for github webhooks integration and more effective automated builds.
