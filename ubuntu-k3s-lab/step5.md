# Configuração dos recursos Kubernetes
## Definição dos Services e Ingress
### Configuração de Service para o Wordpress
TBD
* Cria o arquivo YAML com as configurações do Persistent Volume Claims
```bash
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
* Cria o arquivo YAML com as configurações do Persistent Volume Claims
```bash
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
--- 
# Configuração dos recursos Kubernetes
## Aplicação das configurações
TBD
```bash
# Aplicar a configuração de PVC (wordpress-pvc)
kubectl apply -f wordpress-pvc.yaml
# Aplicar a configuração de PVC (mysql-pvc)
kubectl apply -f mysql-pvc.yaml
# Aplicar a configuração de Deployment (wordpress-deployment)
kubectl apply -f wordpress-deployment.yaml
# Aplicar a configuração de Deployment (mysql-deployment)
kubectl apply -f mysql-deployment.yaml
# Aplicar a configuração de Service (wordpress-service)
kubectl apply -f wordpress-service.yaml
# Aplicar a configuração de Service (mysql-service)
kubectl apply -f mysql-service.yaml
# Aplicar a configuração de Ingress (wordpress-ingress)
kubectl apply -f wordpress-ingress.yaml
```{{exec}}

Para aplicar todos os arquivos .yaml da pasta corrente, utilizar o seguinte comando:
```bash
kubectl apply -f .
```{{exec}}

  