## Configuração de Persistent Volume Claims (PVCs)
Nesta etapa serão criados os arquivos YAML com as configurações do Persistent Volume Claims (PVCs). Cada PVC é responsável por armazenar os dados e arquivos de um ou mais pods do cluster. Essas configurações são essenciais para manter a persistência e a integridade dos dados do cluster.

### Configuração de Persistent Volume Claims do WordPress
Criar o arquivo YAML com as configurações do Persistent Volume Claims

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

> Para fechar e salvar um arquivo no editor Nano, primeiro digite **CTRL + X** e quando as opções forem exibidas na parte inferior do editor, digite **Y** e em seguida **Enter**.
> Antes de salvar os arquivos no editor Nano, certifique-se que o foco do cursor está ativo no editor.

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

> Para fechar e salvar um arquivo no editor Nano, primeiro digite **CTRL + X** e quando as opções forem exibidas na parte inferior do editor, digite **Y** e em seguida **Enter**.
> Antes de salvar os arquivos no editor Nano, certifique-se que o foco do cursor está ativo no editor.