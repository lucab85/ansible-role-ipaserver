# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    config.vm.synced_folder '.', '/vagrant', disabled: true
    config.vm.boot_timeout = 1800
    config.vm.define "ipa", primary: true do |ipa|
        ipa.vm.hostname = "ipa.example.com"
        ipa.vm.box = "generic/rhel8"
        ipa.vm.provider "virtualbox" do |v|
            v.memory = "4096"
            v.cpus = 2
            v.linked_clone = true
            v.customize ["modifyvm", :id, "--pagefusion", "on"]
            v.customize ["modifyvm", :id, "--nictype1", "Am79C973"]
            v.customize ['modifyvm', :id, '--cableconnected1', 'on']
        end
    end

  config.vm.provision "ansible" do |ansible|
    ansible.galaxy_role_file = 'playbooks/requirements.yml'
    ansible.playbook = "playbooks/provision.yml"
#    ansible.ask_vault_pass = true
  end
end
