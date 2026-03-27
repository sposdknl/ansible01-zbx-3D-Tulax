# Definice proměnné s názvem boxu
IMAGE_NAME = "bento/ubuntu-24.04"

Vagrant.configure("2") do |config|
  # Globální nastavení pro všechny VM
  config.vm.box = IMAGE_NAME
  config.vm.box_architecture = "amd64"   # nutné pro Intel/AMD

  # Globální provider nastavení (výchozí hodnoty)
  config.vm.provider "virtualbox" do |vb|
    vb.memory = 2048
    vb.cpus = 2
  end

  # Definice stroje "bastion"
  config.vm.define "bastion" do |bastion|
    bastion.vm.hostname = "bastion"
    bastion.vm.network "private_network", ip: "192.168.1.12", virtualbox__intnet: "zabbix"

    # Přepis nastavení providera pro tento konkrétní stroj
    bastion.vm.provider "virtualbox" do |v|
      v.memory = 1024
      v.name = "Bastion-ansible2"
    end

    # Provisioning pomocí Ansible (lokálně nainstalovaného ve VM)
    bastion.vm.provision "ansible_local" do |ansible|
      ansible.playbook = "ansible_provision.yml"
      ansible.install_mode = "default"
    end
  end
end