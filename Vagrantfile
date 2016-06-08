# -*- mode: ruby -*-
# vi: set ft=ruby :

$fix_vmware_tools_script = <<SCRIPT
if [ -s /etc/vmware-tools/locations ]; then
  sed -i.bak 's/answer AUTO_KMODS_ENABLED_ANSWER no/answer AUTO_KMODS_ENABLED_ANSWER yes/g' /etc/vmware-tools/locations
  sed -i 's/answer AUTO_KMODS_ENABLED no/answer AUTO_KMODS_ENABLED yes/g' /etc/vmware-tools/locations
fi
SCRIPT

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
  config.vm.provision "shell", inline: "apt-get install -y python aptitude"

  config.vm.provision "shell", inline: $fix_vmware_tools_script

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "scripts/setup-box.yml"
  end

  config.vm.provision "reload"
  
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "scripts/setup-box-step-2.yml"
  end

  config.vm.box = "puppetlabs/ubuntu-14.04-64-nocm"

  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
    v.cpus = 2
  end

  config.vm.boot_timeout = 600
end
