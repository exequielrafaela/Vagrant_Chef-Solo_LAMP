# Vagrant_Chef-Solo_LAMP
*_Chef Solo is used to provision and configures commonly used software in a LAMP Satck_*

*In this repo you'll find the Vagrant file and all the necessary files to provision an Ubuntu VM lauched vía Vagrant+Vbox and provisioned a LAMP (Apache + PHP + MySQL) w/ CHEF, configuration manager tool.*

<p align="center">
  <b>Some Related Links:</b><br>
  <a href="#">https://learn.chef.io/</a> |
  <a href="#">https://supermarket.chef.io/cookbooks/</a> |
  <a href="#">https://goo.gl/j1qW7n</a>
  <br><br>
  <img src="https://github.com/exequielrafaela/Vagrant_Chef-Solo_LAMP/blob/master/images/vagrant_chef.jpg"  width="550" height="300">
</p>

vagrant-linux-apache-mysql-php
==============================

##Chef

The reason Chef is so hard, and the reason it has such as steep learning curve, is that every single blog post or tutorial, and even the chef manual itself, all deal with low-level Chef. That is not what we want. As a developer I have a hundred things to do and no time to do them. I don't care about low-level stuff. I want stuff that Just Works. So here we go. This is the least amount of knowledge you need to get a lamp stack up and running on Vagrant. As a side effect of that, you'll actually learn quite a bit of Chef along the way.

### Key Points

Before we start, there are a couple of key definitions you're going to need to learn to make your life simpler. They aren't difficult, and I'll do my best to distil them down to a basic level.

### Cookbooks

Installing things (apache, mysql, php etc) is done by something called Cookbooks. Cookbooks are a collection of Templates and Recipes (and a few other things we don't care about right now) that tell Chef how to install something.

### Recipes

At a basic level, a Recipe is a ruby file that calls a bunch of Chef functions to install something.

### Templates

A template is much like a PHP app template with variable replacements, loops etc, but for system config files. Think v-hosts, httpd.conf, php.ini etc.

### LWRP

You will see LWRPs mentioned a lot and it's not immediately obvious what they are. It stands for Light Weight Resource Providers. But really they're functions that do something Chefy (like install a Pecl Module/PEAR Library in the PHP Cookbook). They should just call them that. You don't really need to use these yet, but I figured you'd want to know what they are when you see them mentioned elsewhere.

### Chef Server vs Chef Solo

Chef comes in two flavours. Chef Solo and Chef Server. Chef is always run on the guest or machine being provisioned, not your own machine or workstation. That means it needs to have the cookbooks copied across in order for it to know where they are. Chef Server takes care of this for you (the copying across), as well as managing a central repository of your cookbooks.

Chef Server can also do some other fancy stuff (such as provisioning new EC2 instances for you), but unless you're using it for a live server or professional dev-ops (and we're not), forget about it. We can copy the cookbooks across ourselves (or in reality vagrant will).

One final point of note: Opscode (the company behaind chef) will host a Chef server for you, or you can do it yourself. It would appear Chef can provision it's own Chef Server, but I've not tried.

### Roles

A role is simply a type of server. E.g. If you have a distributed architecture with a load balancer, 2x web servers and 2x database servers, your roles would be "Load Balancer", "Web Server", and "Database Server". That's a role.

A role is not limiting, in reality it's a name given to a collection of cookbooks you want to run. E.g. You specify that your webserver roll should run the apache, php, and mysql cookbooks. The cookbooks that a particular role should run is called a "Run List" in Chef, that's because the name of the Chef function you pass the cookbooks to run to is run_list.

### Nodes and Data Bags

You don't need to know about this, but I will cover it here for completeness. Chef also has the concepts of "Nodes" and "Data-Bags". I haven't used these features, but my understanding is that a "Node" is an instance of a Role. So you have your 2x webservers, each using the "Web Server" role. Each one of those is a Node.

From my understanding, "Data-Bags" provide additional data to your Recipes, this could be a list of admins or databases to create, or something similar. I haven't used them, so I'm not familiar with them.

___________________

Chef Solo is used to provision and configures the following sofware that are commonly used in a LAMP Satck:

## cookbooks

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

## roles - at this time a single role was created for both WEB and DB. 
Will breakout the role in future update for expanssion and growth. DB credentials are stored in this file also to setup
roles/vagrant-test-box.rb

## recipes - setup apache2 vhosts in file 
site-cookbooks/apache2/recipes/vhosts.rb

**Tested with Host OS:** Ubuntu 14.04.4 LTS x64 (and same vagrant box  "ubuntu/trusty64" version)

**Tested with Vagrant: Vagrant 1.8.5
**Test
	vagrant-berkshelf (4.1.0) (OPTIONAL)
	vagrant-hostmanager (1.8.5) (REQUIRED)
	vagrant-omnibus (1.4.1) (REQUIRED)
	vagrant-share (1.1.5, system) (REQUIRED)


## Getting Started
A quick way to get started is with Vagrant and VirtualBox.

### Requirements
- [Vagrant](http://www.vagrantup.com/downloads.html)
- [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
- 
### Chef Files and tree directory structure
The files are configured to use a tree directory structure as you can see below.
So consider that it's a must to uncompress Vagrant_Chef-Solo_LAMP/chef-archive/chef.tar.gz in ../chef.

For example:

~/vagrant_projects$ tree -L 2
.                                                                                                                                                                                   
├── chef                                                                                                                                                                            
│   ├── cookbooks                                                                                                                                                                   
│   ├── data_bags                                                                                                                                                                   
│   ├── nodes                                                                                                                                                                       
│   ├── roles                                                                                                                                                                       
│   └── site-cookbooks                                                                                                                                                              
├── Vagrant_Chef-Solo_LAMP                                                                                                                                                          
│   ├── chef-archive                                                                                                                                                                
│   ├── data                                                                                                                                                                        
│   ├── images                                                                                                                                                                      
│   ├── LICENSE                                                                                                                                                                     
│   ├── README.md                                                                                                                                                                   
│   ├── site                                                                                                                                                                        
│   ├── Vagrantfile                                                                                                                                                                 
│   └── Vagrantfile.chef                                                                                                                                                            

## To trigger VAGRANT:
	vagrant up
```
Wait a few minutes for the server to be created and provisioned.  Access the app by going to this URL: http://www.example.vm/index.php
```

### Additional vagrant commands
**SSH to the box**

	vagrant ssh
```
**Re-provision the box to apply the changes you made to the Ansible configuration**
```
	vagrant provision
```
**Reboot the box**
```
	vagrant reload
```
**Shutdown the box**
```
	vagrant halt

