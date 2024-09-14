# Testes de Resiliência
TBD.

### Simulação da perda dos pods do MySQL
Liste os pods em execução no cluster, dessa vez filtrando pelos pods do MySQL.

```bash
kubectl get pods | grep mysql
```{{exec}}

Em seguida, apagamos os pods do MySQL com o comando abaixo:

```bash
kubectl delete pods $(kubectl get pods -o json | jq -r '.items[] | select(.metadata.name | test("mysql-")).metadata.name')
```{{exec}}

### Verificação da integridade dos dados do MySQL
Para verificar a integridade dos pods removidos, acesse novamente ou atualize o site WordPress para verificar o comportamento.
