# curso_ansible
Curso de Ansible realizado na Udemy - Professor Phillipe Costa

# Pré-requisitos:

## Conhecimentos básicos em Sistemas Operacionais Linux
  * Manipulação de arquivos/diretórios
  * Instalação de pacotes
  * Configurações de redes (IP, DNS, Gateway)
  
## Conhecimentos básicos em Sistemas oepracionais M$ Windows

## Conhecimentos básicos de virtualização com Virtual BOX (cou outro Hypervisor)
  * Crição  de VM (Virtual Machine)
  * Configurações de rede
  * Criação de clones
  
O que é Ansible?

Ansible é uma ferramenta Open Source que possibilita a comunicação e intereção com diversos destinos ao mesmo tempo. Foi desenvolvido por Michael DeHann (Red Hat)

Principais vertentes: Gerenciamento de Mudança,  provisionamento, automação e orquestração

O principal arquivo de configuração do ansible é o ansble.cfg. Sua localização padrão é: /etc/ansible/ansible.cfg.As alterações e configurações são interpretadas na seguinte ordem:

  * Variável de ambiente ANSIBLE_CONFIG
  * ansbeble.cfg no diretório corrente
  * .ansible.cfg no diretório home
  * /etc/ansible/ansible.cfg
 
