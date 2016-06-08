# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  # FIXME This is a third-party dependency (the NSA is watching!)
  config.vm.box = "ubuntu/trusty64"
  config.vm.network :private_network, ip: "192.168.24.48"
  config.vm.network :forwarded_port, guest: 80, host: 9990
  config.vm.network :forwarded_port, guest: 443, host: 9991
  config.vm.hostname = 'qa-automation.local'
  config.vm.provider "virtualbox" do |v|
    v.memory = 1024 * 4
    v.cpus = 1
  end

  # Provision the machine using an ansible playbook.
  # See documenation at:
  #  - http://docs.ansible.com/guide_vagrant.html
  #  - https://docs.vagrantup.com/v2/provisioning/ansible.html
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "#{ENV['playbook'] || 'vagrant.yml'}"
    ansible.inventory_path = "#{ENV['inventory'] || 'vagrant-inventory'}"
    ansible.limit = 'all'  # The special 'all' group name.
    ansible.verbose = 'vvv'
  end
end
