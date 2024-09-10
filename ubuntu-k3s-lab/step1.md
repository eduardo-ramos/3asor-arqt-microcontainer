
# Resolução do Trabalho
Antes de mergulharmos na configuração e execução de um cluster Kubernetes em um ambiente Ubuntu Linux, é crucial estabelecer uma base sólida. Este capítulo aborda os pré-requisitos essenciais para garantir que sua máquina virtual (VM) esteja pronta para o processo.

## Pré-requisitos
### Atualizar o sistema operacional
Run `sudo apt-get update`{{exec}}

Com esses pré-requisitos atendidos, sua VM estará pronta para iniciar a configuração do cluster Kubernetes. A seguir, exploraremos os passos detalhados para a criação e gerenciamento do seu cluster.

# Configuração do Kubernetes
## Instalação do Docker
O Kubernetes usa o Docker como mecanismo de contêiner por padrão. Verifique se o Docker está devidamente instalado na máquina virtual que está sendo usada com o seguinte comando:

```bash
docker -v
```{{exec}}

O resultado deverá ser parecido com o exemplo abaixo, do contrário, será necessário instalar o Docker para seguir adiante.

```bash
Docker version 20.10.22, build 3a2c30b
```

Para instalar o Docker, utilize os comandos a seguir:

```bash
sudo apt-get install docker.io -y
sudo systemctl enable docker
sudo systemctl start docker
```{{exec}}

### Instalação do kubeadm, kubelet e kubectl
Kubelet, kubeadm e kubectl são as ferramentas necessárias para criar e gerenciar seu cluster K8S. Através destas ferramentas é possível criar pods, deployments, services, persistent volumes, entre outros recursos utilizados em um cluster.

### Instalação do k3s
Uma alternativa é instalar a ferramenta k3s da CNCF para criar e gerenciar o cluster K8S. O k3s simplifica a criação de clusters K8S, pois traz consigo as ferramentas kubelet, kubeadm e kubectl.
Execute os comandos abaixo no terminal do Ubuntu para instalar o k3s:

* Acessar usuário root
`sudo su`{{exec}}

* Instalar K3S com kubectl
```bash
curl -sfL https://get.k3s.io | sh -
echo K3S_KUBECONFIG_MODE=\"644\" >> /etc/systemd/system/k3s.service.env
```{{exec}}

* Restart do serviço k3s para carregar nova config
`systemctl restart k3s`{{exec}}

Em seguida, verifique se o cluster está funcionando, executando o comando abaixo no terminal do Ubuntu para obter as informações dos nós do cluster K8S
`kubectl get nodes`{{exec}}

## Criação do diretório de trabalho

Navegue para a pasta do usuário ubuntu
```bash
cd ~
```{{exec}}

Depois, crie o diretório de trabalho para armazenar os arquivos de configuração do cluster e navegue para o diretório criado com o comando anterior.
```bash
mkdir k8s-cluster`{{exec}}
cd k8s-cluster
```{{exec}}

## Configuração de Persistent Volume Claims (PVCs)
### Configuração de Persistent Volume Claims do WordPress
* Criar o arquivo YAML com as configurações do Persistent Volume Claims
`nano wordpress-pvc.yaml`{{exec}}

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: wordpress-pvc
  labels:
    app: wordpress
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: local-path
  resources:
    requests:
      storage: 1Gi
```{{copy}}

Para fechar e salvar, primeiro digite ctrl + X e quando as opções forem exibidas na parte inferior do editor Nano, digite Y e Enter.

### Configuração de Persistent Volume Claims do MySQL
* Criar o arquivo YAML com as configurações do Persistent Volume Claims
`nano mysql-pvc.yaml`{{exec}}

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mysql-pvc
  labels:
    app: mysql
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: local-path
  resources:
    requests:
      storage: 1Gi
```{{copy}}

## Configurações de deployment

### Configuração de Deployment do WordPress

TBD

```bash
# Cria o arquivo YAML com as configurações do Persistent Volume Claims
nano wordpress-deployment.yaml
```{{exec}}

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: wordpress-deployment
  labels:
    app: wordpress
spec:
  replicas: 3
  selector:
    matchLabels:
      app: wordpress
  template:
    metadata:
      labels:
        app: wordpress
    spec:
      containers:
        - name: wordpress-container
          image: wordpress:php8.3-apache
          imagePullPolicy: "Always"
          ports:
            - containerPort: 80
              name: http-port
          env:
            - name: WORDPRESS_DB_HOST
              value: mysql-service.default.svc.cluster.local
            - name: WORDPRESS_DB_USER
              value: db-user
            - name: WORDPRESS_DB_PASSWORD
              value: db-pass
            - name: WORDPRESS_DB_NAME
              value: wordpress-db
          volumeMounts:
            - mountPath: /etc/www/html
              name: wordpress-volume
      volumes:
        - name: wordpress-volume
          persistentVolumeClaim:
            claimName: wordpress-pvc
      securityContext:
        fsGroup: 0 
        runAsUser: 0
```{{copy}}

  

### Configuração de Deployment do MySQL

TBD

```bash
# Cria o arquivo YAML com as configurações do Persistent Volume Claims
nano mysql-deployment.yaml
```{{exec}}

```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: mysql-statefulset
  labels:
    app: mysql 
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
        - name: mysql-container
          image: mysql:8.0 
          imagePullPolicy: "Always" 
          ports:
            - containerPort: 3306 
              name: mysql-port 
          env: 
            - name: MYSQL_USER
              value: db-user
            - name: MYSQL_PASSWORD
              value: db-pass
            - name: MYSQL_DATABASE
              value: wordpress-db
            - name: MYSQL_ROOT_PASSWORD
              value: password
          volumeMounts:
            - mountPath: /var/lib/mysql
              name: mysql-volume 
      volumes: 
        - name: mysql-volume 
          persistentVolumeClaim:
            claimName: mysql-pvc 
      securityContext:
        fsGroup: 0 
        runAsUser: 0 
```{{copy}}

## Definição dos Services e Ingress

### Configuração de Service para o Wordpress

TBD

```bash
# Cria o arquivo YAML com as configurações do Persistent Volume Claims
nano wordpress-service.yaml
```{{exec}}

```yaml
apiVersion: v1
kind: Service
metadata:
  name: wordpress-service 
  labels:
    app: wordpress 
spec:
  selector:
    app: wordpress 
  ports:
  - name: http-sv-port 
    port: http-port 
    targetPort: http-port
```{{exec}}

### Configuração de Service para o MySQL

TBD

```bash
# Cria o arquivo YAML com as configurações do Persistent Volume Claims
nano mysql-service.yaml
```{{exec}}


```yaml
apiVersion: v1
kind: Service
metadata:
  name: mysql-service 
  labels:
    app: mysql 
spec:
  selector:
    app: mysql 
  ports:
  - name: http-sv-port 
    port: mysql-port 
    targetPort: mysql-port
```{{exec}}

  

### Configuração de Ingress para exposição do Wordpress

TBD

```bash
# Cria o arquivo YAML com as configurações do Persistent Volume Claims
nano wordpress-ingress.yaml
```{{exec}}

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress 
metadata:
  name: wordpress-ingress
spec:
  rules:
  - http:
      paths:
      - path: / 
        pathType: Prefix 
        backend:
          service:
            name: wordpress-service 
            port:
              number: 80 
```{{exec}}

```yaml
# Aplicar a configuração de PVC (hello-world-pvc)
kubectl apply -f wordpress-pvc.yaml
# Aplicar a configuração de PVC (hello-world-pvc)
kubectl apply -f mysql-pvc.yaml
# Aplicar a configuração de Deployment (hello-world-deployment)
kubectl apply -f wordpress-deployment.yaml
# Aplicar a configuração de Deployment (hello-world-deployment)
kubectl apply -f mysql-deployment.yaml
# Aplicar a configuração de Service (hello-world-service)
kubectl apply -f wordpress-service.yaml
# Aplicar a configuração de Service (hello-world-service)
kubectl apply -f mysql-service.yaml
# Aplicar a configuração de Ingress (hello-world-ingress)
kubectl apply -f wordpress-ingress.yaml

# Para aplicar todos os arquivos .yaml da pasta corrente, utilizar o seginte comando:
kubectl apply -f .
```{{exec}}

  