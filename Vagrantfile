# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|

  config.vm.box = "hashicorp/bionic64"
  config.vm.provider "virtualbox" do |v|
    v.name = "VM to flash firmware into ProMicro"
    v.customize ["modifyvm", :id, "--usb", "on"]
    v.customize ["modifyvm", :id, "--usbehci", "on"]
    # Please rewrite according to your environment. VID/PID is required.
    v.customize ["usbfilter", "add", "0",
                 "--target", :id,
                 "--name", "Arduino Micro (writable)",
                 "--vendorid", "2341",
                 "--productid", "0037",
                 "--remote", "no"]
    v.customize ["usbfilter", "add", "1",
                 "--target", :id,
                 "--name", "Arduino Micro",
                 "--vendorid", "2341",
                 "--productid", "8037",
                 "--remote", "no"]
  end

  # I used local qmk_firmware repository.
  # Please rewrite according to your environment.
  config.vm.synced_folder "/Users/ben/Projects/qmk_firmware", "/qmk_firmware"
  config.vbguest.auto_update = true

  # Install build tools
  config.vm.provision "shell", privileged: false, inline: <<-SHELL 
    sudo apt-get update
    sudo apt-get install -y python3-pip avrdude
    /qmk_firmware/util/qmk_install.sh
   SHELL
end
