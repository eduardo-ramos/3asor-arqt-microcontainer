# Testes de Resiliência
## Simulação da perda de pods
Os testes a seguir irão simular a perda de pods do cluster, com o objetivo de testar a recuperação automática dos serviços e se os dados persistidos mantém a consistência.

> Para a realização desses testes, antes é necessário instalar a ferramenta jq, que permite interagir com arquivos e textos em formato json através do shell do Linux.

```bash
$ Linha de comando para a instalação do jq
sudo apt install -y jq
```{{exec}}

O resultado após a instalação deverá ser similar ao exemplo abaixo:

```bash
ubuntu@ubuntu:~/k8s-cluster$ sudo apt install -y jq
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following NEW packages will be installed:
  jq
0 upgraded, 1 newly installed, 0 to remove and 178 not upgraded.
Need to get 50.2 kB of archives.
After this operation, 99.3 kB of additional disk space will be used.
Get:1 http://archive.ubuntu.com/ubuntu focal-updates/universe amd64 jq amd64 1.6-1ubuntu0.20.04.1 [50.2 kB]
Fetched 50.2 kB in 0s (144 kB/s)
Selecting previously unselected package jq.
(Reading database ... 72837 files and directories currently installed.)
Preparing to unpack .../jq_1.6-1ubuntu0.20.04.1_amd64.deb ...
Unpacking jq (1.6-1ubuntu0.20.04.1) ...
Setting up jq (1.6-1ubuntu0.20.04.1) ...
Processing triggers for man-db (2.9.1-1) ...
```