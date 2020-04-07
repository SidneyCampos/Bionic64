# -*- mode: ruby -*-
# vi: set ft=ruby :
$script_mysql = <<-SCRIPT
  apt-get update && \
  apt-get install -y mysql-server-5.7 && \
  mysql -e "create user 'phpuser'@'%' identified by 'pass';"
SCRIPT


Vagrant.configure("2") do |config|
	config.vm.box = "hashicorp/bionic64"
  config.vm.box_version = "1.0.282"
	
  config.vm.network "forwarded_port", guest: 80, host: 8089
	config.vm.network "public_network", ip: "192.168.0.200"
	
  config.vm.provision "shell",
  inline: "cat /configs/id_bionic64.pub >> .ssh/authorized_keys"

  config.vm.provision "shell", inline: $script_mysql

  config.vm.provision "shell", inline: "cat /configs/mysqld.cnf > /etc/mysql/mysql.conf.d/mysqld.cnf"

  config.vm.provision "shell", inline: "service mysql restart"

  config.vm.provision "shell", 
  inline: "apt-get install -y nginx"

  config.vm.synced_folder "./configs", "/configs"
  config.vm.synced_folder ".", "/vagrant", disabled:true

	config.vm.provider "virtualbox" do |vb|
		vb.memory = "4096"
	end
end
  # ---------------- Others commands

# Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

# Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

# Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   apt-get update
  #   apt-get install -y apache2
  # SHELL


