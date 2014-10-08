# Setup script for Sentry on CentOS 6.x
[![Gitter](https://badges.gitter.im/Join Chat.svg)](https://gitter.im/milesich/setup-sentry-centos?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

[Sentry](https://getsentry.com/welcome/) is a realtime event logging and aggregation platform.<br>
This scrips provides you to setup Sentry on CentOS 6.x with MySQL and Redis as Queue/Buffer/Cache so quickly.

## Specification

* Sentry
  * Queue: Redis
  * Buffer: Redis
  * Cache: Redis
  * work directory: /var/sentry
  * Persistent DB: MySQL (user/pass:sentry)
  * daemonize: Supervisord
  * execute user: sentry

## Usage

#### General Usage

```sh
# install git and patch first because they are missing on centos
$ sudo yum install git patch

$ sudo git clone https://github.com/y-ken/setup-sentry-centos.git /usr/local/src/sentry/
$ cd /usr/local/src/sentry/

# execute setup script
$ sudo sh setup_sentry.sh

# edit SENTRY_URL_PREFIX
$ sudo vi /etc/sentry.conf.py

# execute middleware
$ sudo service redis start
$ sudo service mysqld start
$ sudo service supervisord start

# access the url like below.
$ curl localhost:9000
```

#### Docker

Run with Linux Container named [Docker](https://www.docker.io/) is also supported for instant testing.<br>
It is useful to access with ssh port-forwarding to your local machine after execute `docker run`.

```sh
# install and run docker process if you have not already used docker
$ sudo yum -y install docker-io --enablerepo=epel
$ sudo service docker start

# clone repository
$ git clone https://github.com/y-ken/setup-sentry-centos.git
$ cd setup-sentry-centos

# build machine
$ sudo docker build -rm -t sentry .

# execute machine
$ DOCKER_MACHINE=`sudo docker run -d -t sentry`

# login to the machine (user/pass:root)
$ sudo docker inspect $DOCKER_MACHINE | grep IPAddress
$ ssh root@what-are-you-have-saw-the-IPAddress

# establish a port forward connection against the remote server
$ ssh -L 9000:172.17.0.8:9000 user@your-vps-server # execute at local machine

# open url with your web browser
# URL: http://localhost:9000
```

#### Vagrant

```sh
$ git clone https://github.com/y-ken/setup-sentry-centos.git
$ cd setup-sentry-centos

# execute machine
$ vagrant up

# login to the machine
$ vagrant ssh
```

## TODO

Pull requests are very welcome!!

## Copyright

Copyright © 2014- Kentaro Yoshida ([@yoshi_ken](https://twitter.com/yoshi_ken))

## License

* MIT License http://www.opensource.org/licenses/mit-license.php
