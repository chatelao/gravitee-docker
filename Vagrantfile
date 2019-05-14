# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|

  # start --olc
  config.vbguest.auto_update = false
  config.vbguest.auto_reboot = false
  # stop  --olc

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  # an alternative to this Ubuntu 14.04 box is the "v0rtex/xenial64" with the 16.04 LTS
  # config.vm.box = "ubuntu/trusty64" 
  config.vm.box = "bento/centos-7.6" 

  # access a port on your host machine (via localhost) and have all data forwarded to a port on the guest machine.
  config.vm.network "forwarded_port", guest: 8000, host: 81
  config.vm.network "forwarded_port", guest: 8002, host: 82
  config.vm.network "forwarded_port", guest: 8005, host: 83

  config.vm.network "private_network", ip: "192.168.99.50", virtualbox__intnet: false

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network "private_network", ip: "192.168.188.110"
  #define a larger than default (40GB) disksize
  config.disksize.size = '50GB'
  
  config.vm.provider "virtualbox" do |vb|
    vb.name = 'docker-compose-vm'
    vb.memory = 4096
    vb.cpus = 1
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end

  # install docker & docker-compose into the VM 
  # run the docker-compose.yml file - if it exists -  whenever the  VM starts (https://github.com/leighmcculloch/vagrant-docker-compose)
  config.vm.provision :docker
  config.vm.provision :docker_compose, yml: "/vagrant/environments/demo/docker-compose-local.yml", run: "always"
  
  # config.vm.provision :docker_compose
  # config.vm.provision "shell", inline: "/vagrant/provision.sh"

  # Specify registry mirrors to use - $ENGINE_REGISTRY_MIRROR = localhost:5000

end
