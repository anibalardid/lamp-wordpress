# -*- mode: ruby -*-
# vi: set ft=ruby :
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.hostname = "lamp-wordpress.local"
  config.vm.network :private_network, ip: "192.168.100.102"

  config.vm.provider :virtualbox do |vb|
    vb.name = "lamp-wordpress"
    vb.memory = 512
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--ioapic", "on"]
    vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end

  # Ansible provisioner.
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/playbook.yml"
    ansible.limit = 'all'
    ansible.sudo = true
  end

  # Sync Data Folder
  config.vm.synced_folder "data/", "/var/www/", owner: "www-data", group: "www-data"
end
