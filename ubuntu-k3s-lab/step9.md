# Testes de Resiliência
### Simulação da perda dos pods do MySQL
Assim como a simulação da perda de pods do WordPress, a simulação da perda de pods do MySQL tem por objetivo garantir que tanto o Wordpress, quanto o MySQL continuem funcionando normalmente após a perda de seus pods.

Mesmo que os pods do MySQL sejam deletados, o Wordpress deve continuar funcionando normalmente após o MySQL se restabelecer.

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
