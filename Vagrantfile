# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    config.vm.synced_folder '.', '/vagrant', disabled: true
    config.vm.define "ipa", primary: true do |ipa|
        ipa.vm.hostname = "ipa.example.com"
        ipa.vm.box = "generic/rhel8"
        ipa.vm.network "public_network", bridge: "wlp61s0", use_dhcp_assigned_default_route: true, ip: "192.168.0.98"
        ipa.vm.provider "virtualbox" do |v|
            v.memory = "4096"
            v.cpus = 2
            v.linked_clone = true
            v.customize ["modifyvm", :id, "--pagefusion", "on"]
        end
    end

  config.vm.provision "ansible" do |ansible|
    ansible.galaxy_role_file = 'playbooks/requirements.yml'
    ansible.playbook = "playbooks/provision.yml"
#    ansible.ask_vault_pass = true
  end
end
