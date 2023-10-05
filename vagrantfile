# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "gusztavvargadr/ubuntu-server"

  config.vm.define "server1" do |server1|
    
    server1.vm.network "private_network", ip: "192.168.56.1", gateway: "192.168.56.3"
    config.vm.synced_folder ".", "/var/www/html"
    config.vm.provision "shell", inline: <<-SHELL
       apt-get update
      sudo apt install apache2 -y
    SHELL
    
    
  end
  config.vm.define "server2" do |server2|
    config.vm.network "private_network", ip: "192.168.56.2", gateway: "192.168.56.3"
    config.vm.provision "shell", inline: <<-SHELL
     apt-get update
    sudo apt install mysql-server -y
    SHELL
  
  end

  config.vm.define "server3" do |server3|
   
    config.vm.network "private_network", ip: "192.168.56.3"
    config.vm.network "public_network", type: "dhcp", bridge: "wlp3s0"
    config.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get -y install net-tools
      sudo sysctl -w net.ipv4.ip_forward=1
      sudo iptables -t nat -A POSTROUTING -o enp0s3 -j MASQUERADE
      SHELL

  end

end

