# 

Vagrant.configure("2") do |masterConfig|
  #VM1: master
  masterConfig.vm.define "master" do |master|
    master.vm.box = "oraclelinux/8"
    master.vm.hostname = "master"
    master.vm.network "private_network", ip: "192.168.20.10"
    master.vm.network "forwarded_port", guest:80, host: 80
    master.vm.network "forwarded_port", guest:443, host: 443
    master.ssh.insert_key = false
    master.vm.provider "virtualbox" do |vMaster|
      vMaster.name = "ansible_master"
      vMaster.customize ["modifyvm", :id, "--memory", 4096]
      vMaster.customize ["modifyvm", :id, "--cpus", 2]
    end
    master.vm.provision "shell", inline: <<-SHELL
      dnf update
      dnf groupinstall -y 'Minimal Install'
      dnf install -y vim mc
      echo "192.168.20.10 master master" >> /etc/hosts
      echo "192.168.20.12 node1 node1" >> /etc/hosts
      echo "192.168.20.14 node2 node2" >> /etc/hosts
      echo "192.168.20.16 node3 node3" >> /etc/hosts
      echo "!!! Konfiguracja sshd !!!"
      sed -i '/GSSAPIAuthentication/ s/^/#/' /etc/ssh/sshd_config
      sed -i '/GSSAPICleanupCredentials/ s/^/#/' /etc/ssh/sshd_config
      sed -i -e 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
      echo "!!! Restart sshd !!!"
      systemctl restart sshd
    SHELL
  end
end

Vagrant.configure("2") do |node1Config|
  #VM2: Node1
  node1Config.vm.define "node1" do |node1|
    node1.vm.box = "oraclelinux/8"
    node1.vm.hostname = "node1"
    node1.vm.network :private_network, ip: "192.168.20.12"
    node1.ssh.insert_key = false
    node1.vm.provider "virtualbox" do |vNode1|
      vNode1.name = "ansible_node1"
      vNode1.customize ["modifyvm", :id, "--memory", 3072]
      vNode1.customize ["modifyvm", :id, "--cpus", 2]
    end
    node1.vm.provision "shell", inline: <<-SHELL
      echo "192.168.20.10 master master" >> /etc/hosts
      echo "192.168.20.12 node1 node1" >> /etc/hosts
      echo "192.168.20.14 node2 node2" >> /etc/hosts
      echo "192.168.20.16 node3 node3" >> /etc/hosts
      echo "!!! Konfiguracja sshd !!!"
      sed -i '/GSSAPICleanupCredentials/ s/^/#/' /etc/ssh/sshd_config
      sed -i -e 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
      echo "!!! Restart sshd !!!"
      systemctl restart sshd
    SHELL
  end
end

Vagrant.configure("2") do |node2Config|
  #VM3: Node2
  node2Config.vm.define "node2" do |node2|
    node2.vm.box = "oraclelinux/8"
    node2.vm.hostname = "node2"
    node2.vm.network :private_network, ip: "192.168.20.14"
    node2.ssh.insert_key = false
    node2.vm.provider "virtualbox" do |vNode2|
      vNode2.name = "ansible_node2"
      vNode2.customize ["modifyvm", :id, "--memory", 3072]
      vNode2.customize ["modifyvm", :id, "--cpus", 2]
    end
    node2.vm.provision "shell", inline: <<-SHELL
      echo "192.168.20.10 master master" >> /etc/hosts
      echo "192.168.20.12 node1 node1" >> /etc/hosts
      echo "192.168.20.14 node2 node2" >> /etc/hosts
      echo "192.168.20.16 node3 node3" >> /etc/hosts
      echo "!!! Konfiguracja sshd !!!"
      sed -i '/GSSAPICleanupCredentials/ s/^/#/' /etc/ssh/sshd_config
      sed -i -e 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
      echo "!!! Restart sshd !!!"
      systemctl restart sshd
    SHELL
  end
end

Vagrant.configure("2") do |node3Config|
  #VM4: Node3
  node3Config.vm.define "node3" do |node3|
    node3.vm.box = "oraclelinux/8"
    node3.vm.hostname = "node3"
    node3.vm.network :private_network, ip: "192.168.20.16"
    node3.ssh.insert_key = false
    node3.vm.provider "virtualbox" do |vNode3|
      vNode3.name = "ansible_node3"
      vNode3.customize ["modifyvm", :id, "--memory", 3072]
      vNode3.customize ["modifyvm", :id, "--cpus", 2]
    end
    node3.vm.provision "shell", inline: <<-SHELL
      echo "192.168.20.10 master master" >> /etc/hosts
      echo "192.168.20.12 node1 node1" >> /etc/hosts
      echo "192.168.20.14 node2 node2" >> /etc/hosts
      echo "192.168.20.16 node3 node3" >> /etc/hosts
      echo "!!! Konfiguracja sshd !!!"
      sed -i '/GSSAPICleanupCredentials/ s/^/#/' /etc/ssh/sshd_config
      sed -i -e 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
      echo "!!! Restart sshd !!!"
      systemctl restart sshd
    SHELL
  end
end
