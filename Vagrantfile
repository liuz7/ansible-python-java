# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define "ubuntu" do |ubuntu|
    ubuntu.vm.box = "ubuntu/trusty64"
    ubuntu.vm.hostname = 'ubuntu'
    ubuntu.vm.box_url = "ubuntu/trusty64"
    ubuntu.vm.box_check_update = false

    ubuntu.vm.network :private_network, ip: "192.168.56.101"
    ubuntu.vm.network :forwarded_port, guest: 22, host: 10122, id: "ssh"
    ubuntu.vm.synced_folder "..", "/vagrant_data/workspace"

    ubuntu.vm.provision :ansible do |ansible|
        ansible.playbook = "playbook.yml"
    end

    ubuntu.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 2048]
      v.customize ["modifyvm", :id, "--name", "ubuntu"]
    end
  end

  config.vm.define "centos" do |centos|
    #centos.vm.box = "puphpet/centos65-x64"
    centos.vm.box = "centos67-x64"
    centos.vm.hostname = 'centos'
    #centos.vm.box_url = "puphpet/centos65-x64"
    centos.vm.box_url = "http://192.168.7.101/software/vagrant/centos/origin/centos67-x64.box"
    centos.vm.box_check_update = false

    centos.vm.network :private_network, ip: "192.168.56.102"
    centos.vm.network :forwarded_port, guest: 22, host: 10222, id: "ssh"
    centos.vm.synced_folder "..", "/vagrant_data/workspace"

    centos.vm.provision :ansible do |ansible|
        ansible.playbook = "playbook.yml"
    end

    centos.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 2048]
      v.customize ["modifyvm", :id, "--name", "centos"]
    end
  end

end
