# -*- mode: ruby -*-oringlogs
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  config.vm.provision "file", source: "files/monlog.pub", destination: "/home/vagrant/.ssh/"

  config.vm.define "controlnode" do |controlnode|
    controlnode.vm.box = "ubuntu/focal64"
    controlnode.vm.hostname = "controlnode"
    controlnode.vm.network "private_network", ip: "192.168.56.6"
    controlnode.vm.synced_folder "./ansible","/home/vagrant/ansible"
    controlnode.vm.provision "file", source: "files/monlog", destination: "/home/vagrant/.ssh/"
    controlnode.vm.provision "shell", inline: <<-SHELL
      sed -i 's/ChallengeResponseAuthentication no/ChallengeResponseAuthentication yes/#g' /etc/ssh/sshd_config
      service ssh restart
      sudo apt update && sudo apt --assume-yes install ansible
      chmod 600 /home/vagrant/.ssh/monlog
      chmod 644 /home/vagrant/.ssh/monlog.pub
    SHELL
  end

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.define "monlog" do |monlog|
    monlog.vm.box = "bento/centos-7.5"
    monlog.vm.hostname = "monlog-server"
    monlog.vbguest.auto_update = false
    monlog.vm.network "private_network", ip: "192.168.56.7"
    monlog.vm.provision "shell", inline: <<-SHELL
      cat /home/vagrant/.ssh/monlog.pub >> /home/vagrant/.ssh/authorized_keys
    SHELL
  end

end
