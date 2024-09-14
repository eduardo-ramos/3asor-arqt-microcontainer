## Definição dos Services e Ingress
Services e Ingress permitem que os usuários sejam capazes de acessar os recursos do cluster K8S.
O Service permitem que um pod seja exposto de forma que possam ser acessados por outros pods.
Já a configuração de Ingress permite que o acesso seja feito por um IP ou um nome de domínio.

### Configuração de Service para o Wordpress
Cria o arquivo YAML com as configurações de Service para o Wordpress.

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
```{{exec}}

> Para fechar e salvar um arquivo no editor Nano, primeiro digite **CTRL + X** e quando as opções forem exibidas na parte inferior do editor, digite **Y** e em seguida **Enter**.
> Antes de salvar os arquivos no editor Nano, certifique-se que o foco do cursor está ativo no editor.

### Configuração de Service para o MySQL
Cria o arquivo YAML com as configurações de Service para o MySQL.

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

> Para fechar e salvar um arquivo no editor Nano, primeiro digite **CTRL + X** e quando as opções forem exibidas na parte inferior do editor, digite **Y** e em seguida **Enter**.
> Antes de salvar os arquivos no editor Nano, certifique-se que o foco do cursor está ativo no editor.

### Configuração de Ingress para exposição do Wordpress
Cria o arquivo YAML com as configurações de Ingress para exposição do Wordpress.

```bash
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
