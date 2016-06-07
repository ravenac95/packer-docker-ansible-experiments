# -*- mode: ruby -*-
# vi: set ft=ruby :

# WARNING!
# This is the Vagrant file used for packaging. For the file used to test look
# in the tests directory

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
#  config.vm.provision "shell", inline: "apt-get install -y python aptitude"
#
#  config.vm.provision "ansible" do |ansible|
#    ansible.playbook = "scripts/setup-box.yml"
#  end
#
#  # Install latest guest additions
#  config.vm.provider "virtualbox" do |v|
#    config.vm.provision "shell", inline: "apt-get install virtualbox-guest-additions-iso"
#  end
#
#  config.vm.provision "reload"
  
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "scripts/setup-box-step-2.yml"
  end

  #config.vm.box = "ubuntu/xenial64"
  config.vm.box = "puppetlabs/ubuntu-14.04-64-nocm"


  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
    v.cpus = 2

    path_to_disk = './.vagrant/tmp_disk.vdi'

    unless File.exists?( path_to_disk )
      # Need to have a 20G /tmp directory
      v.customize ['createhd', '--filename', path_to_disk, '--format', 'VDI', '--size', 15 * 1024]
      v.customize ['storageattach', :id, '--storagectl', 'IDE Controller', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', path_to_disk]
    end
  end

  #config.vm.synced_folder ".", "/vagrant/"

  config.vm.boot_timeout = 600
end
