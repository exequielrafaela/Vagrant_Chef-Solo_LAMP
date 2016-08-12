# Vagrant_Chef-Solo_LAMP
*_Chef Solo is used to provision and configures commonly used software in a LAMP Satck_*

*In this repo you'll find the Vagrant file and all the necessary files to provision an Ubuntu VM lauched vía Vagrant+Vbox and provisioned a LAMP (Apache + PHP + MySQL) w/ CHEF, configuration manager tool.*

<p align="center">
  <b>Some Related Links:</b><br>
  <a href="#">https://learn.chef.io/</a> |
  <a href="#">https://supermarket.chef.io/cookbooks/</a> |
  <a href="#">https://goo.gl/j1qW7n</a>
  <br><br>
  <img src="https://github.com/exequielrafaela/Vagrant_Chef-Solo_LAMP/blob/master/images/vagrant_chef.jpg"  width="200" height="300">
</p>

vagrant-linux-apache-mysql-php
==============================

====================

Chef Solo is used to provision and configures the following sofware that are commonly used in a LAMP Satck:

cookbooks
===================
- apache2
- apt
- build-essential
- chef-sugar
- chef_handler
- iis
- iptables
- logrotate
- memcached
- mysql
- openssl
- php
- runit
- windows
- xml
- yum
- yum-epel
- yum-mysql-community

roles - at this time a single role was created for both WEB and DB. Will breakout the role in future update for expanssion and growth. DB credentials are stored in this file also to setup
=========================
roles/vagrant-test-box.rb

recipes - setup apache2 vhosts in file 
===============================
site-cookbooks/apache2/recipes/vhosts.rb

**Tested with OS:** Ubuntu 12.04.4 LTS x64

**Tested with Vagrant: Vagrant 1.6.3
**Test

	vagrant-berkshelf (3.0.1) (optional) not used at this time
	vagrant-hostmanager (1.5.0) (required) - adds a host entry to your loacl machine for www.example.vm for 192.168.33.10
	vagrant-login (1.0.1, system) (optional)
	vagrant-omnibus (1.4.1) (required) - ensures using the latest version of chef (can be slow to download at provisioning  
	vagrant-share (1.1.1, system) (required)


URL To Test once Vagrant is up and running: http://www.example.vm/index.php
C


## Getting Started
A quick way to get started is with Vagrant and VirtualBox.

### Requirements
- [Vagrant](http://www.vagrantup.com/downloads.html)
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)

vagrant up
```

Wait a few minutes for the server to be created and provisioned.  Access the app by going to this URL: http://www.example.vm/index.php

### Additional vagrant commands
**SSH to the box**
```
vagrant ssh
```

**Re-provision the box to apply the changes you made to the Ansible configuration**
```
vagrant provision

**Reboot the box**
```
vagrant reload
```

**Shutdown the box**
```
vagrant halt
```
