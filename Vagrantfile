# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  # Box Settings
  config.vm.box = "marianoRafael/nativescript"

  # Provide Settings
  config.vm.provider "virtualbox" do |vb|
    vb.memory = 2048
    vb.cpus = 2

    # Allow Debugging through physical device
    vb.customize ["modifyvm", :id, "--usb", "on"]
  end

  # Netword Settings
  config.vm.network "private_network", ip: "192.168.33.10"

  # Folder Settings
  config.vm.synced_folder ".", "/app",
    type:"nfs",
    mount_options: %w{rw,async,nolock,vers=3}

end
