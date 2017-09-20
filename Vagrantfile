# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "ubuntu/xenial64"

  # Network - Host Updator
  config.vm.network :private_network, ip: "192.168.33.33"
  #config.vm.network :public_network, ip: "192.168.11.123", bridge: "en1: Wi-Fi (AirPort)"
  # config.vm.network :public_network, ip: "192.168.11.123", bridge: "en0: Ethernet"
  config.vm.hostname =  "ubuntu.localdev"

  # config.vm.synced_folder "./www-public", "/var/www/www-public", type: 'nfs'
  #config.vm.synced_folder "./share_data", "/share_data", type: 'nfs'

  # Provisioning
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook/site.yml"
    ansible.inventory_path = "playbook/hosts"
    ansible.limit = 'all'
  end

  config.vm.provider :virtualbox do |v|
    v.name = "ubuntu.localdev"

    # Chipset (Supposedly better CPU performance)
    v.customize [ "modifyvm", :id, "--chipset", "ich9" ]

    # Network
    v.customize ["modifyvm", :id, "--cableconnected1", "on"]

    # CPU up to 4 cores and ioapic
    v.customize ["modifyvm", :id, "--ioapic", "on"]
    v.customize ["modifyvm", :id, "--cpus", "2"]
    v.customize ["modifyvm", :id, "--pae", "on"]
    v.customize ["modifyvm", :id, "--natdnsproxy1", "off"]
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "off"]
    v.customize ["modifyvm", :id, "--paravirtprovider", "kvm"]
    v.customize ["modifyvm", :id, "--memory", "1024"]

    # Time setting
    v.customize ["setextradata", :id, "VBoxInternal/Devices/VMMDev/0/Config/GetHostTimeDisabled", 1]

    # SSD Settings
#    v.customize ["storagectl", :id, "--name", "SCSI", "--controller", "IntelAHCI", "--portcount", "1", "--hostiocache", "on"]
#    v.customize ["storageattach", :id, "--storagectl", "SCSI", "--port", "0", "--device", "0", "--nonrotational", "on"]
  end
end
