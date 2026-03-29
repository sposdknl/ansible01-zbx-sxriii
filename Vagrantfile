# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|config.vm.boot_timeout = 300

  config.vm.define "bastion-ansible" do |bastion|
    bastion.vm.box = "bento/ubuntu-24.04"
    bastion.vm.hostname = "bastion-ansible"

    # NAT síť (výchozí – pro přístup k internetu a apt balíčkům)
    # eth0 je automaticky NAT

    # Host-only síť – MUSÍ být ve stejné podsíti jako eth1 Zabbix Appliance
    # Zabbix Appliance eth1: 192.168.56.10
    # Bastion:               192.168.56.20
    bastion.vm.network "private_network", ip: "192.168.56.20"

    bastion.vm.provider "virtualbox" do |vb|
      vb.name   = "Bastion-ansible"
      vb.memory = "2048"
vb.gui = true
      vb.cpus   = 2
    end

    # Provisioning – naklonuje repo a nainstaluje Ansible
    bastion.vm.provision "shell", inline: <<-SHELL
      apt-get update -y
      apt-get install -y ansible git python3-pip

      # Vytvoř adresář a naklonuj repo
      mkdir -p /opt/repo
      # Klonování provede ansible_provision.yml (viz Ansible playbook)
    SHELL
  end

end
