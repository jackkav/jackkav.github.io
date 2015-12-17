---
layout: post
title:  "Graphicsmagick Docker Meteor"
date:   2015-11-09 00:57:38 +0800
categories: graphicsmagick docker meteor
---
Adding graphicsmagick to your docker apt-get install is essentially all that is required to use the tool in your app, however graphicsmagick throws an error on use which doesn't seem to affect its results but can be easily fixed with the addition of libicu48
{% highlight docker %}
  FROM philipgraf/meteor-pdf
  MAINTAINER Jack Kavanagh <jack.kavanagh@digitalpublishing.cn>
  RUN apt-get update \
          && apt-get install -y --no-install-recommends \
                  openjdk-7-jre-headless \
                  graphicsmagick \
                  libicu48 \
          && rm -rf /var/lib/apt/lists/*
{% endhighlight %}
