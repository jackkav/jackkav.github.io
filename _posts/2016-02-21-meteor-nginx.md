---
layout: post
title:  "Nginx Docker Meteor"
date:   2016-02-21 00:57:38 +0800
categories: nginx docker meteor
---

So here it is the config necessary to get your meteor server running through nginx.

Let's assume you have a server running docker and your meteor container is present at 192.168.0.10:88

You'll need an nginx.conf and am nginx docker container. Be sure to put your nginx config in the path below at ~/nginx/nginx.conf so that docker can map it to the container config.
I've also included an example redirect by subdomain.

{% highlight bash %}
docker run -d --name nginx -p 80:80 -v ~/nginx/nginx.conf:/etc/nginx/nginx.conf:ro nginx
{% endhighlight %}

{% highlight bash %}
user  nginx;
worker_processes  1;
error_log  /var/log/nginx/error.log warn;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024;
}

http {
    # configure backend Meteor servers
    # one line per instance
    upstream meteor_server {
        server 192.168.0.10:88; #local ip and port of meteor docker instance
        ip_hash;
    }

    ## actual site configuration
    server {
        server_name www.mydomain.com;
        client_max_body_size 80M;
        ## performance boost using gzip
        gzip on;
        gzip_disable "msie6";
        gzip_vary on;
        gzip_proxied any;
        gzip_comp_level 6;
        gzip_types text/plain text/css application/json application/x-javascript text/xml application/xml application/xml+rss text/javascript;
        # end of GZIP block

        ## this is the actual load balancing to the meteor backend servers
        location / {
            proxy_pass http://meteor_server; # the name used in upstreams, substituted for any of the defined instances
            proxy_redirect off;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header Host $http_host;
            # Make sure to use WebSockets
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection "upgrade";
        }
    }
    ## example redirect to url by subdomain
    server {
      server_name abc.mydomain.com;
      return 301 "http://www.mydomain.com/abc";
    }
}
{% endhighlight %}
