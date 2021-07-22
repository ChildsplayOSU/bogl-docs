---
sort: 5 # Order in the sidebar
---

# Deployment

In this section we'll discuss the final aspect of the BoGL stack, the live deployment that is hosted at bogl.engr.oregonstate.edu.

Jumping right into it, the live deployment runs on an AWS EC2 instance. On this instance we run boglserver behind an [NGINX](https://nginx.org/en/) webserver that routes requests to and from boglserver. The EC2 instance itself is reachable via an [AWS elastic IP](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html) that has been fixed to this EC2 instance. We have also worked with OSU's IT department to point the 4th level domain bogl.engr.oregonstate.edu to this IP, giving us the ability to serve a non-OSU server through an OSU domain. We use an outside server instead of OSU's equipment due to their restrictions on running custom servers. There are no limitations to how many deployments we could have, but this primary one has proven to be the most successful at making BoGL accessible. The AWS account itself is managed by OSU's IT department, but has several BoGL teammembers connected to it for management.

## AWS

![Live Deployment of BoGL](../imgs/h7.jpeg "Live Deployment of BoGL")

If you are going to be doing dev-ops on the EC2 instance, you should be familiar with working in the command line, and you should also have familiarity with working on Amazon's framework. You should take some time to read some more about working with [EC2 instances](https://aws.amazon.com/ec2/getting-started/), which can be helpful for understanding how to work with this setup.

The first thing you'll need to be able to do is access the server directly via ssh. In order to do this, you can request to have yourself added to the shared AWS account using our account ID and contacting coe.support@oregonstate.edu, or you can ask an existing team-member with access (like Dr. Parham-Mocello) to login via https://login.oregonstate.edu/apps/aws/ and grant you access to the server. The primary **ubuntu** user account is what is used to control most of the system features, and you should be able to ask any teammember with access to have yourself added to this account as needed.
```bash
ssh ubuntu@bogl.engr.oregonstate.edu
# or
ssh yourotheracct@bogl.engr.oregonstate.edu
```

Generally, you'll want to have access to the server under **ubuntu** as well as having access to the AWS control panel (through the login link mentioned above). Once logged in, the AWS control panel is used to stop, start, and reconfigure instances. Since the account is shared there are other instances as well, so you will want to look for the instance tagged with the name **ACTIVE_BoGL_Box**, which i the live deployment. Another instance named **Dev_BoGL_Box** is a similar environment used for testing new changes that might be risky on the live environment. You shouldn't need to interact with any of the other boxes, and be considerate as there may be other students working on the same account!

If you're ever creating new instances or modifying things, make sure to tag whatever assets are used with 'bogl' or something similar so we can keep track of it.

In the future, if issues of the server not being powerful enough to keep up with request volume come up, the instance can be stopped and reprovisioned at a larger size. As of writing this, the current instance is provisioned as **t2.small**, giving it **2 GiB** memory. This may not seem like much, but the server is very light, and doesn't require much to operate normally. Most requests are very quick to evaluate, and the memory pressure from evaluation is generally not very high, but it may be worthwhile considering a larger instance size later on.

As a quick aside, it may be in the best interest in the future to attempt to build a client-side version of BoGL, removing the need to have a language server. This may be achievable using WASM, but has not been investigated seriously yet.

## General Management

Once you're setup on the EC2 instance there are a couple of scripts that you can use to manage BoGL:
- updating boglserver
  - can be done using the script `fireup.sh` from `/home/ubuntu/` (this is akin to the rebuild-reboot.sh script in the [scripts repo](https://github.com/The-Code-In-Sheep-s-Clothing/bogl-deploy-scripts))
- update the website (bogl-editor)
  - also can be done via `fireup.sh`
- restarting boglserver
  - `auto_restart.sh` from `/home/ubuntu/`, which reboots the server without rebuilding anything

As a note, when rebooting the entire AWS instance itself, the server and related functionality will automatically reboot itself as well.

In rare cases, you may find that there is a 'configuration' error or a similar message when trying to reach the bogl website. If this occurs, it's often associated with a subtle issue in NGINX. Running `nginx -s reload` as root is usually sufficient to reset the error. If this still doesn't resolve the error, and you can determine that `boglserver` is running normally by checking its local **test** endpoint, you will need to [inspect the logs](https://logtail.com/tutorials/how-to-view-and-configure-nginx-access-error-logs/) associated with nginx to see if there is a configuration error. If there is, and nginx won't reload or reboot, you can often see the specific issue outlined there.

In relation to the above, the nginx configuration that determines how to serve the BoGL website and server API together is done via the `/etc/nginx/sites-available/bogl_engr_oregonstate_edu` configuration file (note, this file requires root access to modify). Unless you are reworking the API, changing the caching behavior, or some other server related adjustment, you will probably not need to work with this.

NGINX itself can be a lot to work with, so if you're unfamiliar we recommend going through their documentation to understand [what it is and how it works](https://www.nginx.com/resources/wiki/start/). Even if you're not planning to do any configuration changes, it's helpful to at least know how to stop, start, and reload nginx.
```bash
# start nginx if isn't running already
nginx

# reload with any new configuration changes
# also tends to refresh the server, and iron out
# any issues that have popped up
nginx -s reload

# stop the nginx process (you will probably not need this one)
nginx -s stop
```

## Maintaining the SSL Certificate

You may have been wondering why we have *two* web servers, boglserver and nginx. We have both so we can secure the communication between the client and our AWS instance, especially since the users of BoGL are a mix of students and teachers. There are two connections, one from the client to NGINX, and another from NGINX to boglserver. Given that the connection from NGINX to boglserver is conducted locally on the same machine, the connection we need to secure is the one that exists from the client to NGINX; the one over the internet and outside our AWS box. Additionally, implementing SSL/TLS support via Servant by hand is unlikely to be as reliable as trusting a well established and dedicated web server application. This is *especially* critical considering that users may be minors, and as such their data needs to be protected.

The SSL certificate used to secure the connection to bogl.engr.oregonstate.edu is issued from [Lets Encrypt](https://letsencrypt.org/), a non-profit CA that has been issuing quality certificates for some time now. They have a command line utility that we use periodically to update our certs, which is done automatically. However, in the event that the cert is not renewed on time, you can also renew it by hand.
```bash
# renew any local certs via 'certbot'
# this should renew our issued cert for bogl.engr.oregonstate.edu
certbot renew

# reload nginx to apply the renewed certs
nginx -s reload
```
If the cert was outdated, this should immediately rectify the issue. In most cases, this should not be a problem, but it is important to keep in mind how to do this.

## Updating the Documentation

The documentation you're reading now is also held on the same site, but in a different location under **nelsonai**'s account. You can update the documentation by running the following commands as that user in their home folder.
```bash
# specifically use the following ruby version
# does not work from a script...
rvm use 2.7.1

# update the docs normally
./update_docs.sh
```

Since the docs are cloned via git, this repo is locked to only working with that user locally, but if the reader has the time this could be moved to the ubuntu user as well while also changing the NGINX routing configuration for the docs.

## Server Keep-Alive

Despite maintenance and updating, sometimes instances will need to be rebooted. This a normal part of the life cycle of any process. Part of this is due to the unpredictability of incoming requests and their content that the server receives over time. In order to prevent unforeseen issues from requests crashing the server, there is a CRON job that keeps the server alive. It's a simple solution, but it works quite well.
```bash
# auto reboot every minute
* * * * * /home/ubuntu/./auto_restart.sh >> /home/ubuntu/restarts.log
```
Even if someone manages to create a runaway BoGL program, or if the server simply exhausts itself, this will ensure it stays alive. To inspect this, you can use `crontab -e` from the ubuntu account.

## Automatic Updates

As a final note, having to maintain the server by hand can be a bit tiresome. To get around this, we setup an automatic update that pulls down the latest version of **bogl** and the **bogl-editor** to update the server and the website together every morning at 3 AM. This is also done in CRON job.
```bash
# shuts down and restarts everything at 3:00 AM PST (the server is 7 hours ahead PST), allows new updates to reach the server
0 10 * * * /home/ubuntu/./fireup.sh >> /home/ubuntu/restarts.log
```
For the most part, due to the keep-alive and the automatic nightly update, the BoGL stack is relatively maintenance free. It only needs to be watched periodically to make sure everything is okay. Running a simple expression like `5` in the editor online and seeing a correct response is sufficient to check that everything is working as expected.
