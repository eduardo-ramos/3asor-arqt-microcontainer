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
    port: 80 
    targetPort: 80

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
    port: 3306 
    targetPort: 3306
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
