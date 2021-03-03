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
 
 No arquivo ansible.cfg estão as configurações mais enxutas que foram usadas no curso
 
 ## Arquivo de inventário - hosts -
 
 É o arquivo de inventário que contem todos os hosts que serão alvos das modificações do ansible. Por padrão este arquivo já é criado na instalação do ansible e fica disponível no diretório /etc/ansible/hosts, porém pode-se criar o arquivo em outro diretório. O que muda é que na chamada do ansible deve-se explicitar o diretório. Caso não seja especificado, o ansible irá ler o arquivo hosts dentro de /etc/ansible/hosts.  No arquivo hosts vai todos os ips ou fdqn's dos hosts alvos, um por linha. EX:
 
192.168.1.2
192.168.1.3
192.168.1.4
 
Também é possível separar os hosts alvos por grupos. Cada grupo deve ser criado usando: [NOME_DO_GRUPO]. EX:

[servidoresWeb]
192.168.1.2
192.168.1.3

[servidoresBanco]
192.168.1.4

Há também a possibilidade de criar sub-grupos. EX:

[servidoresWeb]
192.168.1.2
192.168.1.3

[servidoresBanco]
192.168.1.4

[servidores:children]
servidoresWeb

 
A linha de comando passando o arquivo hosts é: 

ansible -i hosts all -m ping (para todos os hosts)
ansible -i hosts servidoresWeb -m ping (para todos os hosts do servidoresWeb)
ansible -i hosts servidores -m ping (para todos os grupos do sub-grupo servidores)


Explicando a linha de comando: 

ansible - autoexplicativo (kkk)
-i - Especifica o arquivo de inventario a ser usado
hosts - Nome do arquivo de inventario que está sendo utilizado
all - Siguinifica que todos as maquinas alvo descritas no arquivo de inventário serão contempladas pelo comando
servidoresWeb - Nome do grupo algo que está dentro do arquivo hosts
servidores - Nome do subgrupo algo que está dentro do arquivo hosts
-m - Especifíca o módulo que será utilizado
ping - Nome do módulo utilizado

Existe também a opção de trabalhar com variáveis simples e variáveis por GRUPO no arquivo hosts:

#VARIÁVEIS POR GRUPO:
[servidoresWeb:vars]
ansible_ssh_port=22
ansible_ssh_user=root
ansible_ssh_pass=123456
ansible_become=yes
ansible_become_method=sudo


#VARIÁVEIS SIMPLES:
[servidoresWeb]
apache1 ansible_ssh_host=192.168.1.2
apache2 ansible_ssh_host=192.168.1.3
 
 
 ## Roles -
 
 É o conjunto de intens independentes destinados a provisionar uma determinada aplicação/infraestrutura.
 Itens:
 Variáveis;
 Módulos;
 Tarefas;
 Ações;
 É possível associar roles com projetos.
 
 IMPORTANTE: As roles possuem uma estrutura padrão de diretórios para os projetos:
 
#playbooks
site.yml
webservers.yml
fooservers.yml
roles/
    common/ #Este é o projeto
        tasks/ #Lista de tarefas para serem executadas em uma role
        handlers/ #eventos acionados por uma task
        files/ #arquivos utilizados para deploy dentro de uma role
        templates/ #Modelos para deploy dentro de uma role (permite uso de variaveis)
        vars/ #Variáveis adicionais de uma role
        defaults/ #Variáveis padrão de uma role. Prioridade máxima
        meta/ #Trata dependências de uma role por outra role - Primeiro diretório a ser analizado
        

IMPORTANTE: Dentro dos diretórios tasks, handlers, vars, defaults e meta deverá existir um arquivo com o nome de main.yml para que o mesmo seja interpretado 
 
## Variáveis -

Existe uma 'Ordem de Precedência' para a interpretação de variáveis no ansbile (na documentação a lista está em ordem de predecêdencia do menor para o maior):

https://docs.ansible.com/ansible/latest/user_guide/playbooks_variables.html

As variáveis são geralente utilizadas para facilitar no provisionamento dos sistemas/infraestrutura. Entretanto, o ansible permite através  do  módulo setup  obter  o  que  chamamos  de Systems Facts. Os  Systems  Facts  são  descobertos  pelo  ansible  através  do  módulo setup, trazendo informações de todo o sistema.

Exemplo: ansible hostname -m setup 

## Variáveis no arquivo de inventário (hosts) -

apache1 ansible_ssh_host=192.168.1.2
apache2 ansible_ssh_host=192.168.1.3
 
## tasks -

Tarefas responsáveis por executar ações em uma determinada role. Lembrando que dentro do diretório /tasks de ter um arquivo chamado main.yml onde estarão efetivamente nossas tarefas.
Exemplo de uma task para instalar o pacote vim utilizando o módulo apt:

![image](https://user-images.githubusercontent.com/50958562/109834320-d0465500-7c20-11eb-817d-d8f8e68028a9.png)



        
