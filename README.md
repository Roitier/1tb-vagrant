# Configuração do Vagrant para Ambiente de Servidores

Este é um exemplo de arquivo de configuração do Vagrant que cria um ambiente de servidores utilizando três máquinas virtuais.

## Requisitos

- Vagrant instalado (https://www.vagrantup.com/)
- Box "gusztavvargadr/ubuntu-server" disponível (você pode ajustar a box conforme necessário)

## Configuração

1. Clone este repositório.
2. Navegue até o diretório onde o arquivo Vagrantfile está localizado.

## Uso
pode ter diferenças de acordo com o sistema operacional do usuario.
1. Execute o comando `vagrant up` para iniciar as máquinas virtuais.
2. Aguarde até que o Vagrant provisione as máquinas e realize as configurações necessárias.
3. Após a conclusão, você poderá acessar as máquinas virtuais usando o comando `vagrant ssh <nome-da-maquina>`, substituindo <nome-da-maquina> pelo nome da máquina virtual desejada.

