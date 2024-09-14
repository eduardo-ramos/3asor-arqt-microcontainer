## Configuração de Persistent Volume Claims (PVCs)
### Configuração de Persistent Volume Claims do WordPress
* Criar o arquivo YAML com as configurações do Persistent Volume Claims

```bash
nano wordpress-pvc.yaml
```{{exec}}

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
```{{exec}}

Para fechar e salvar, primeiro digite ctrl + X e quando as opções forem exibidas na parte inferior do editor Nano, digite Y e Enter.

### Configuração de Persistent Volume Claims do MySQL
Criar o arquivo YAML com as configurações do Persistent Volume Claims
```bash
nano mysql-pvc.yaml
```{{exec}}

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
```{{exec}}
