# -*- mode: ruby -*-
# vi: set ft=ruby :
# launching three node(VM's)locally to launch nginx in web node
# pre requisites: virtual box, ansible, install vagrant on your pc, go to this directory, vagrant validate template and
# vagrant up to run these nodes

Vagrant.configure("2") do |config|


  config.vm.define "web" do |virtualbox|
    virtualbox.vm.hostname = "web"
    virtualbox.vm.box = "generic/rhel7"
    virtualbox.vm.network :private_network, ip: "192.168.2.101"
    virtualbox.vm.network :forwarded_port, guest: 22, host: 10122, id: "ssh"
 

    virtualbox.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 512]
      v.customize ["modifyvm", :id, "--name", "web"]
    end

  end
  
  config.vm.define "app-node1" do |virtualbox|
    virtualbox.vm.hostname = "app-node1"
    virtualbox.vm.box = "generic/rhel7"
    virtualbox.vm.network :private_network, ip: "192.168.2.102"
    virtualbox.vm.network :forwarded_port, guest: 22, host: 10222, id: "ssh"
    virtualbox.vm.network :forwarded_port, guest: 80, host: 8484

    virtualbox.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 512]
      v.customize ["modifyvm", :id, "--name", "app-node1"]
    end

  end

  config.vm.define "app-node2" do |virtualbox|
    virtualbox.vm.hostname = "app-node2"
    virtualbox.vm.box = "generic/rhel7"
    virtualbox.vm.network :private_network, ip: "192.168.2.103"
    virtualbox.vm.network :forwarded_port, guest: 22, host: 10322, id: "ssh"
    virtualbox.vm.network :forwarded_port, guest: 80, host: 8484

    virtualbox.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 512]
      v.customize ["modifyvm", :id, "--name", "app-node2"]
    end

  end

  config.vm.provision "ansible" do |ansible|
    
    ansible.groups = {
      "app" => ["app-node1", "app-node2"],
      "web" => ["web"]
    }

    ansible.verbose = "v"
    ansible.playbook = "playbook.yml"
  end

end
