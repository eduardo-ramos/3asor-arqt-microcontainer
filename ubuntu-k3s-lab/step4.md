## Configurações de deployment
Nesta etapa serão criados os arquivos YAML com as configurações do Deployment do Kubernetes.
Os Deployments são responsáveis por executar os containers Docker em um cluster.
É atraves deles que são configurados a imagem de um container, as configurações de rede (quando houver), configuração de volumes, variávis de ambiente e entre outros. 

### Configuração de Deployment do WordPress

```bash
# Cria o arquivo YAML com as configurações de Deployment para o WordPress
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
```{{exec}}
  
> Para fechar e salvar um arquivo no editor Nano, primeiro digite **CTRL + X** e quando as opções forem exibidas na parte inferior do editor, digite **Y** e em seguida **Enter**.
> Antes de salvar os arquivos no editor Nano, certifique-se que o foco do cursor está ativo no editor.

### Configuração de Deployment do MySQL

```bash
# Cria o arquivo YAML com as configurações de Deployment para o MySQL
nano mysql-deployment.yaml
```{{exec}}

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql-deployment
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
```{{exec}}
> Para fechar e salvar um arquivo no editor Nano, primeiro digite **CTRL + X** e quando as opções forem exibidas na parte inferior do editor, digite **Y** e em seguida **Enter**.
> Antes de salvar os arquivos no editor Nano, certifique-se que o foco do cursor está ativo no editor.
