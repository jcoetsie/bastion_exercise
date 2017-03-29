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
  # boxes at https://atlas.hashicorp.com/search.

  config.vm.define "web" do |web|
    web.vm.box = "minimal/xenial64"
    web.vm.network "private_network", ip: "192.168.50.11"
  end

  config.vm.define "db" do |db|
    db.vm.box = "minimal/xenial64"
    db.vm.network "private_network", ip: "192.168.50.12"
  end

  config.vm.define "bastion" do |bastion|
    bastion.vm.box = "minimal/xenial64"
    bastion.vm.network "private_network", ip: "192.168.50.10"
    config.vm.network "public_network", bridge: "en0: Wi-Fi (AirPort)"
  end
  

  # take your public key and insert it into the host authorized_keys
  # both for vagrant as for root
  config.ssh.forward_agent    = true
  config.ssh.insert_key       = false
  config.ssh.private_key_path =  ["~/.vagrant.d/insecure_private_key","~/.ssh/id_rsa"]
  config.vm.provision :shell, privileged: false do |s|
    ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
    s.inline = <<-SHELL
      touch /home/$USER/.ssh/authorized_keys
      echo #{ssh_pub_key} >> /home/$USER/.ssh/authorized_keys
    SHELL
  end

end
