VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = 1024
    vb.cpus = 2
  end

  # Assign this VM to a host-only network IP, allowing you to access it
  # via the IP. Host-only networks can talk to the host machine as well as
  # any other machines on the same network, but cannot be accessed (through this
  # network interface) by any external networks.
  config.vm.network "private_network", ip: "192.168.33.33"

  # Use the vagrant hostmaster plugin[^5] to automatically add a domain name
  config.vm.hostname = 'www.example.vm1'
  config.hostmanager.enabled = true
  config.hostmanager.manage_host = true
  #config.hostmanager.ip_resolver = proc do |vm, resolving_vm|
	#  if vm.id
	#	    `VBoxManage guestproperty get #{vm.id} "/VirtualBox/GuestInfo/Net/1/V4/IP"`.split()[1]
	#  end
  #end

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"
  config.vm.synced_folder "./data", "/srv/data"
  config.vm.synced_folder "./site", "/srv/site"

  # Enable provisioning with chef solo, specifying a cookbooks path, roles
  # path, and data_bags path (all relative to this Vagrantfile), and adding
  # some recipes and/or roles.
  config.vm.provision "chef_solo" do |chef|
    chef.verbose_logging = true
    chef.channel = "stable"
    chef.version = "12.10.24"
    chef.custom_config_path = "Vagrantfile.chef"
    chef.cookbooks_path = ["../chef/cookbooks", "../chef/site-cookbooks"]
    #We let know vagrant the role that we've created
    chef.roles_path = "../chef/roles"
    chef.add_role("vagrant-test-box")
    chef.data_bags_path = "../chef/data_bags"
  end
end
