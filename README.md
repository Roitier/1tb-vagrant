 Configuração do Vagrant para Ambiente de Servidores

Este é um exemplo de arquivo de configuração do Vagrant que cria um ambiente de servidores utilizando três máquinas virtuais.

 Requisitos

- Vagrant instalado (https://www.vagrantup.com/)
 
- Box "gusztavvargadr/ubuntu-server" disponível (você pode ajustar a box conforme necessário)

 Configuração

1. Clone este repositório.
  
2. Navegue até o diretório onde o arquivo Vagrantfile está localizado.

 Uso
pode ter diferenças de acordo com o sistema operacional do usuario.
1. Execute o comando `vagrant up` para iniciar as máquinas virtuais.
   
2. Aguarde até que o Vagrant provisione as máquinas e realize as configurações necessárias.
   
3. Após a conclusão, você poderá acessar as máquinas virtuais usando o comando `vagrant ssh <nome-da-maquina>`, substituindo <nome-da-maquina> pelo nome da máquina virtual desejada.

Vagrant.configure("2") do |config|

  config.vm.box = "gusztavvargadr/ubuntu-server"
  
 Inicia a configuração do Vagrant e define a versão da configuração como "2". A partir desta linha, todas as configurações serão feitas dentro deste bloco.
 
 Define a imagem da caixa (box) a ser usada para criar a máquina virtual. Neste caso, a imagem usada é "gusztavvargadr/ubuntu-server". Essa imagem é uma versão personalizada do Ubuntu Server.


  config.vm.define "server1" do |server1|
  
    server1.vm.network "private_network", ip: "192.168.56.1", gateway: "192.168.56.3"
    
    config.vm.synced_folder ".", "/var/www/html"
    
    config.vm.provision "shell", inline: <<-SHELL
    
       apt-get update
       
      sudo apt install apache2 -y
      
    SHELL
    end

  
   A primeira máquina virtual chamada "server1" foi definida.
   
   Configura uma rede privada com IP "192.168.56.1" e gateway "192.168.56.3".
   
   Sincroniza a pasta atual do host com a pasta "/var/www/html" na máquina virtual "server1".
   
   Realiza o provisionamento da máquina virtual "server1" instalando o Apache2.

  config.vm.define "server2" do |server2|
  
    config.vm.network "private_network", ip: "192.168.56.2", gateway: "192.168.56.3"
    
    config.vm.provision "shell", inline: <<-SHELL
    
     apt-get update
     
    sudo apt install mysql-server -y
    
    SHELL
    end
  
   A segunda máquina virtual chamada "server2" foi definida.
   
   Configura uma rede privada com IP "192.168.56.2" e gateway "192.168.56.3".
   
   Realiza o provisionamento da máquina virtual "server2" instalando o MySQL.

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
  
   A terceira máquina virtual chamada "server3" foi definida.
   
   Configura uma rede privada com IP "192.168.56.3".
   
   Configura uma rede pública usando DHCP e a interface de rede "wlp3s0".
   
   Realiza o provisionamento da máquina virtual "server3" instalando algumas ferramentas e realizando algumas configurações.

    sudo sysctl -w net.ipv4.ip_forward=1
   
   faz o roteamento entre diferentes placa de rede

   enp0s3
   É a configuração da placa de rede

    
   
   end
