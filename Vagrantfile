# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Box Settings
  config.vm.box = "generic/debian9"
  # config.vm.box_version = "10.0.0"

  # Provide Settings
  config.vm.provider "virtualbox" do |vb|
    vb.memory = 2048
    vb.cpus = 2

    # Allow Debugging through Android device
    vb.customize ["modifyvm", :id, "--usb", "on"]
    vb.customize ["modifyvm", :id, "--usbehci", "on"]
    vb.customize ["usbfilter", "add", "0", 
    "--target", :id, 
    "--name", "moto g",
    "--manufacturer", "motorola",
    "--product", "Moto G (5) Plus"]
  end

  # Netword Settings
  # config.vm.network "forwarded_port", guest: 5554, host: 5554, host_ip: "127.0.0.1"
  # config.vm.network "forwarded_port", guest: 5555, host: 5555, host_ip: "127.0.0.1"
  # config.vm.network "forwarded_port", guest: 5037, host: 5037, host_ip: "127.0.0.1"

  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
  config.vm.network "private_network", ip: "192.168.33.10"
  # config.vm.network "public_network"

  # Folder Settings
  config.vm.synced_folder ".", "/app",
    type:"nfs",
    mount_options: %w{rw,async,fsc,nolock,vers=3,udp,rsize=32768,wsize=32768,hard,noatime,actimeo=2}

  # Provision Settings
  # config.vm.provision "shell", path: "bootstrap.sh"

end
