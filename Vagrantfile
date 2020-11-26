# -*- mode: ruby -*-
# vi: set ft=ruby :

extra_disk_file = '/tmp/extra_disk.vdi'

Vagrant.configure("2") do |config|

  config.vm.provider "virtualbox"
  config.vm.box = "centos/7"
  config.vm.box_check_update = false
  config.vm.network "forwarded_port", guest: 8080, host: 8080

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = "2048"
    # Create docker lib additional disk
    vb.customize ['createhd', '--filename', extra_disk_file, '--size', 2 * 1024]
    vb.customize ['storageattach', :id, '--storagectl', 'IDE', '--port', 1, '--device', 0, '--type', 'hdd', '--medium', extra_disk_file]
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbooks/00-main.yml"
  end

end
