# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy64"
  config.vm.network "private_network", ip: "10.0.2.104", name: "VirtualBox Host-Only Ethernet Adapter"
  config.vm.network "public_network"
  config.vm.box_download_insecure = true

  # port forwarding
  config.vm.network "forwarded_port", guest: 22, host: 2222

  config.vm.provider "virtualbox" do |v|
    v.memory = 2048
    v.cpus = 2
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end

  config.vm.box_check_update = false
  config.ssh.insert_key = false
  config.vm.provision:shell, inline: <<-SHELL
    echo "root:123456789" | sudo chpasswd
    sudo timedatectl set-timezone Asia/Ho_Chi_Minh
  SHELL
  config.vm.define "ph2-jammy"
  config.vm.hostname = "ph2-jammy"
  config.vm.synced_folder "C:/Data/shared_vagrant", "/home/vagrant/shared_vagrant"
  
  config.vm.provision "shell", inline: <<-SHELL
    ## apt update
    sudo apt-get update -y
    sudo apt-get install -y software-properties-common
    ## install ansible
    sudo -E apt-add-repository ppa:ansible/ansible
    sudo apt-get update -y
    sudo apt-get install -y ansible
  SHELL
  
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "playbook.yml"
  end
end
