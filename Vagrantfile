# -*- mode: ruby -*-
# vi: set ft=ruby :

boxes=[
	{
		:hostname => "web",
		:ip => "192.168.3.11",
		:ports => "8080:80,2211:22",
		:box => "centos/7",
		:ram => 2048,
		:cpu => 1
	},
	{		
		:hostname => "app",
		:ip => "192.168.3.12",
		:ports => "2212:22",
		:box => "centos/7",
		:ram => 2048,
		:cpu => 1
	},
	{
		:hostname => "db",
		:ip => "192.168.3.13",
		:ports => "2213:22",
		:box => "centos/7",
		:ram => 4192,
		:cpu => 1
	}
]

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|

  boxes.each do |box|
	config.vm.define box[:hostname] do |node|
		node.vm.box = box[:box]
		node.vm.network "private_network", ip: box[:ip]
		ports = box[:ports]
		portfwds = ports.split(',', -1)
		portfwds.each do |portfwd|
			host_port = portfwd.split(':')[0]
			guest_port = portfwd.split(':')[1]
			node.vm.network "forwarded_port", guest: guest_port, host: host_port
		end
		node.vm.provider "virtualbox" do |vb|
			vb.customize ["modifyvm", :id, "--memory", box[:ram]]
			vb.customize ["modifyvm", :id, "--cpus", box[:cpu]]
		end
		## Would like to do this but getting Vagrant / Ansible / Windows / and WSL to play 
		## together well is error prone and not worth the effort
#		node.vm.provision :ansible do |ansible|
#			ansible.limit = "all"
#			ansible.playbook = "./ansible/prov_playbook.yml"
#		end
	end
  end
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
#  config.vm.box = "base"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL
end
