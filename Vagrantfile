# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "ubuntu/trusty64"
  config.hostmanager.enabled = true # Must install: vagrant plugin install vagrant-hostmanager

  config.vm.define "zk1.vm" do |node|
    node.vm.network :private_network, :ip => '10.20.1.11'
    config.vm.host_name = "zk1.vm"
  end

  config.vm.define "zk2.vm" do |node|
    node.vm.network :private_network, :ip => '10.20.1.12'
    config.vm.host_name = "zk2.vm"
  end

  config.vm.define "zk3.vm" do |node|
    node.vm.network :private_network, :ip => '10.20.1.13'
    config.vm.host_name = "zk3.vm"
  end

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "./vagrant-ansible.yml"
    ansible.extra_vars = {
        ansible_ssh_user: "vagrant",
        sudo: true
    }
    ansible.host_key_checking = false
    ansible.groups = {
      "zookeeper" => ["zk1.vm", "zk2.vm", "zk3.vm"],
    }
    #ansible.verbose = "vvvv"
    #ansible.hosts = "all"
  end

end
