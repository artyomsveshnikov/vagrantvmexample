# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.



  config.vm.define "vpngateway" do |vpngw|
    vpngw.vm.box = "bento/ubuntu-20.04"
    vpngw.vm.boot_timeout = 200

    vpngw.vm.provider :hyperv do |hyperv|
      hyperv.vmname = "vpngateway"
      hyperv.cpus = 1
      hyperv.memory =  3072
      hyperv.maxmemory = nil
      hyperv.ip_address_timeout = 400
      hyperv.vm_integration_services = {
        guest_service_interface: true,
        heartbeat: true,
        key_value_pair_exchange: true,
        shutdown: true,
        time_synchronization: true
      }
    end
    vpngw.vm.network "public_network", bridge: "Bridge"
    vpngw.vm.synced_folder ".", "/vagrant", disabled: true
    vpngw.ssh.insert_key = false
    vpngw.vm.provision "file", source: "vagrant_machine.pub", destination: "~/.ssh/authorized_keys"
    vpngw.vm.provision "shell", inline: <<-SHELL
      sudo apt update
      sudo apt install -y wget curl zip unzip git build-essential openvpn
    SHELL
  end


  config.vm.define "server" do |server|
    server.vm.box = "bento/ubuntu-20.04"
    server.vm.boot_timeout = 200

    server.vm.provider :hyperv do |hyperv|
      hyperv.vmname = "server"
      hyperv.cpus = 1
      hyperv.memory =  3072
      hyperv.maxmemory = nil
      hyperv.ip_address_timeout = 400
      hyperv.vm_integration_services = {
        guest_service_interface: true,
        heartbeat: true,
        key_value_pair_exchange: true,
        shutdown: true,
        time_synchronization: true
      }
    end
    server.vm.network "public_network", bridge: "Bridge"
    server.vm.synced_folder ".", "/vagrant", disabled: true
    server.ssh.insert_key = false
    server.vm.provision "file", source: "vagrant_machine.pub", destination: "~/.ssh/authorized_keys"
    server.vm.provision "shell", inline: <<-SHELL
      sudo apt update
      sudo apt install -y wget curl zip unzip git build-essential nginx
    SHELL
  end

  config.vm.define "ca" do |ca|
    ca.vm.box = "bento/ubuntu-20.04"
    ca.vm.boot_timeout = 200
    ca.vm.provider :hyperv do |hyperv|
      hyperv.vmname = "ca"
      hyperv.cpus = 1
      hyperv.memory =  3072
      hyperv.maxmemory = nil
      hyperv.ip_address_timeout = 400
      hyperv.vm_integration_services = {
        guest_service_interface: true,
        heartbeat: true,
        key_value_pair_exchange: true,
        shutdown: true,
        time_synchronization: true
      }
    end
    ca.vm.network "public_network", bridge: "Bridge"
    ca.vm.synced_folder ".", "/vagrant", disabled: true
    ca.ssh.insert_key = false
    ca.vm.provision "file", source: "vagrant_machine.pub", destination: "~/.ssh/authorized_keys"
    ca.vm.provision "shell", inline: <<-SHELL
      sudo apt update
      sudo apt install -y wget curl zip unzip git build-essential easy-rsa
    SHELL
  end

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
  
end
