# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Source for the VM
  config.vm.box = "puphpet/ubuntu1404-x64"
  config.vm.hostname = "trusty64"

  # Forwarded ports
  config.vm.network "forwarded_port", guest: 80, host: 8888

  # OpenStack ports
  config.vm.network "forwarded_port", guest: 3333, host: 3333
  config.vm.network "forwarded_port", guest: 5000, host: 5000
  config.vm.network "forwarded_port", guest: 8000, host: 8000
  config.vm.network "forwarded_port", guest: 8004, host: 8004
  config.vm.network "forwarded_port", guest: 8080, host: 8080
  config.vm.network "forwarded_port", guest: 8773, host: 8773
  config.vm.network "forwarded_port", guest: 8774, host: 8774
  config.vm.network "forwarded_port", guest: 8776, host: 8776
  config.vm.network "forwarded_port", guest: 9292, host: 9292
  config.vm.network "forwarded_port", guest: 9696, host: 9696
  config.vm.network "forwarded_port", guest: 35357, host: 35357

  # eth0 - vmnet0
  # This nic is owned/controlled by vagrant.
  # config.vm.network "private_network", ip: "172.16.255.128" #, auto_config: true

  # eth1 - vmnet8
  # This is equivalent to "Private to my mac"
  # The virtual machine is connected to your Mac using
  # a private virtual network. The private network is not
  # normally accessible from the physical networks on
  # the Mac.
  # Multiple virtual machines can be connected to the
  # same private network.
  config.vm.network "private_network", ip: "172.16.40.128" #, auto_config: true

  # A "public_network" config will put a nic on my local
  # network, 192.168.123.x, which I DO NOT want to do.
  # config.vm.network "public_network"

  # If true, then any SSH connections made will enable agent forwarding.
  # Default value: false
  config.ssh.forward_agent = true

  # Disable the new default behavior introduced in Vagrant 1.7, to
  # ensure that all Vagrant machines will use the same SSH key pair.
  # See https://github.com/mitchellh/vagrant/issues/5005
  # config.ssh.insert_key = false

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder "/Users/wchrisjohnson/src/vagrant_data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  config.vm.provider "vmware_fusion" do |v|
    v.gui = false
    v.vmx["memsize"] = "8192"
    v.vmx["numvcpus"] = "2"
    v.vmx["vhv.enable"] = "TRUE"
    # Necessary in Fusion 7 to prevent "Sleep Wake Failure" reboots
    v.vmx["chipset.useAcpiBattery"] = "TRUE"
    v.vmx["chipset.useApmBattery"] = "TRUE"
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/devstack-deploy.yml"
    ansible.verbose = "vv"
  end

end
