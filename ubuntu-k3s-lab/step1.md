## Pré-requisitos
Antes de mergulharmos na configuração e execução de um cluster Kubernetes em um ambiente Ubuntu Linux, é crucial estabelecer uma base sólida. Este capítulo aborda os pré-requisitos essenciais para garantir que sua máquina virtual (VM) esteja pronta para o processo.

### Atualizar o sistema operacional (opcional)
Run `sudo apt-get update`{{exec}}

### Instalação do Docker
O Kubernetes usa o Docker como mecanismo de contêiner por padrão. Verifique se o Docker está devidamente instalado na máquina virtual que está sendo usada com o seguinte comando:

```bash
docker -v
```{{exec}}

O resultado deverá ser parecido com o exemplo abaixo, do contrário, será necessário instalar o Docker para seguir adiante.

```bash
Docker version 24.0.7, build 24.0.7-0ubuntu2~20.04.1
```
<br>
<details>
<summary>Instalação Docker (se necessário)</summary>
<br>

Para instalar o Docker, utilize os comandos a seguir:

```bash
sudo apt-get install docker.io -y
sudo systemctl enable docker
sudo systemctl start docker
```{{exec}}

</details>

Com esses pré-requisitos atendidos, sua VM estará pronta para iniciar a configuração do cluster Kubernetes. A seguir, exploraremos os passos detalhados para a criação e gerenciamento do seu cluster.
