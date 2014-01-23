# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "http://objects.dri.ie/baseboxes/precise64.box"

  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--nictype1", "virtio"]
    vb.customize ["modifyvm", :id, "--nictype2", "virtio"]
    vb.customize ["modifyvm", :id, "--nictype3", "virtio"]
  end

  (0..2).each do |i|
    config.vm.define "node#{i}" do |node|
      node.vm.hostname = "node#{i}.test"
      node.vm.network :private_network, ip: "192.168.251.10#{i}"
      node.vm.network :private_network, ip: "192.168.252.10#{i}"
      (0..1).each do |d|
        node.vm.provider :virtualbox do |vb|
          vb.customize [ "createhd", "--filename", "disk-#{i}-#{d}", "--size", "5000" ]
          vb.customize [ "storageattach", :id, "--storagectl", "SATA Controller", "--port", 3+d, "--device", 0, "--type", "hdd", "--medium", "disk-#{i}-#{d}.vdi" ]
        end
      end
    end
  end

#  config.vm.provision :ansible do |ansible|
#    ansible.playbook =  "site.yml"
#    ansible.inventory_path = "hosts"
#  end

end
