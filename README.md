PHP 7 Development Box
=====================


This repository houses the configuration scripts necessary to build a CentOS 7 based box suitable for PHP7 testing and extension development.

 - Clones latest PHP repository on master branch 
 - Builds from source
 - Installs the compiled binaries as SAPI FPM
 - Includes nginx and PostgreSQL

The configuration is defined in Salt state files. The Salt provisioner can either be run by Packer to generate your own box or by Vagrant to ensure an existing box is running the latest specification. To build the box from scratch yourself, you will require a CentOS 7 ISO that has the minimum software as specified in the kickstarter config or if your internet connection is sufficiently fast you could point it to an ISO image to download.

Packer supports producing VirtualBox and VMware images. Currently the Packer configuration specifies an output VirtualBox machine.

If you do not wish to build the box from source, a pre-built VirtualBox image that can be launched with a single command is provided at [https://atlas.hashicorp.com/rcousens/boxes/php7-dev-c7](https://atlas.hashicorp.com/rcousens/boxes/php7-dev-c7). See [Quick Setup](#quick-setup).

### Packer

> [Packer] is a free and open source tool for creating golden images for multiple platforms from a single source configuration.

### SaltStack


> [SaltStack] is an extremely fast and scalable systems and configuration management software for predictive orchestration, cloud and data center automation, server provisioning, application deployment and more.

## Configuration Files

#### Anaconda KickStarter

Specifies the CentOS 7 installation options and prepares passwordless sudo for vagrant. See [ks.cfg].

#### Packer Provisioning

Installs VirtualBox Guest additions and cleans up post installation. See [scripts] directory and [packer.json].

## Included Components

#### PHP7

PHP7 is the next major release version of PHP. It includes significant performance improvements and additions to the language.

#### nginx

Nginx is installed and configured to serve a website from /srv/www/dev/web. The default dev.conf in /etc/nginx/conf.d/dev.conf contains the configuration.

#### PostgreSQL

PostgreSQL is configured to accept md5 connections from all hosts (I will tighten the security up in the future) with a superuser configured with the login dbuser and password dbuser.

Instructions
------------

## Quick Setup


#### Requirements
* [VirtualBox]
* [Vagrant]

#### Getting Started

Clone this repo into a local directory:
```sh
$ git clone https://github.com/rcousens/packer-php7-dev.git
```
Change directory to where the repo was cloned and launch the vagrant box:
```sh
$ vagrant up
```

##### From the host machine:  
* nginx is listening on localhost port 10001.  
* PostgreSQL is listening on localhost port 10002.

A phpinfo.php script is copied when provisioning that will execute phpinfo. Open up [http://localhost:10001/phpinfo.php](http://localhost:10001/phpinfo.php) in a browser to verify the virtual machine is working and PHP7 has been installed correctly.

##### To access the virtual machine:
```sh
$ vagrant ssh
```

Build Box Yourself
------------------
TODO

Things You Can Do
-----------------

### Run a website with PHP7

Install your website under /srv/www/dev/web with a front controller with the filename app.php.

### Tutorials
* [Compiling PHP Primer][0]
* [Run the PHP7 test suite][1]
* [Debug a PHP extension][2]

License
-------

MIT

[Packer]:https://www.packer.io/
[SaltStack]:http://saltstack.com/
[ks.cfg]:https://github.com/rcousens/packer-php7-dev/blob/master/packer/http/ks.cfg
[scripts]:https://github.com/rcousens/packer-php7-dev/tree/master/packer/scripts
[packer.json]:https://github.com/rcousens/packer-php7-dev/blob/master/packer/packer.json
[Vagrant]:https://www.vagrantup.com/
[VirtualBox]:https://www.virtualbox.org/
[0]:https://github.com/rcousens/packer-php7-dev/blob/master/doc/00-primer-compiling-php.md
[1]:https://github.com/rcousens/packer-php7-dev/blob/master/doc/01-running-tests.md
[2]:https://github.com/rcousens/packer-php7-dev/blob/master/doc/02-debug-php-extension.md

