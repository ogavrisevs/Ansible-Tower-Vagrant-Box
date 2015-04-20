# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "centos_65"
  config.vm.box_url = "https://github.com/2creatives/vagrant-centos/releases/download/v6.5.3/centos65-x86_64-20140116.box"

  config.vm.network "private_network", ip: "192.168.100.1"
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "forwarded_port", guest: 443, host: 8443

  config.vm.provider "virtualbox" do |vb|
     vb.customize ["modifyvm", :id, "--memory", "1024"]
  end

  config.vm.synced_folder "files/", "/root/ansible-tower-config", create: true, owner: "root", group: "root"

  config.vm.provision "shell", inline: "ls -la /root/ansible-tower-config"

  config.vm.provision "shell", inline: "yum install -y ansible tar"
  config.vm.provision "shell", inline: "yum install -y ansible"
  config.vm.provision "shell", inline: "cd /root && curl -O http://releases.ansible.com/ansible-tower/setup/ansible-tower-setup-2.1.3.tar.gz"
  config.vm.provision "shell", inline: "cd /root && tar xvzf ansible-tower-setup-2.1.3.tar.gz"
  config.vm.provision "shell", inline: "cp /root/ansible-tower-config/tower_setup_conf.yml /root/ansible-tower-setup-2.1.3/tower_setup_conf.yml"
  config.vm.provision "shell", inline: "cp /root/ansible-tower-config/inventory /root/ansible-tower-setup-2.1.3/inventory"
  config.vm.provision "shell", inline: "cd /root/ansible-tower-setup-2.1.3 && ./configure -o tower_setup_conf.yml"
  config.vm.provision "shell", inline: "cd /root/ansible-tower-setup-2.1.3 && ./setup.sh"

end
