# Cenário

Você foi contratado para atuar no time DevOps, com a responsabilidade de provisionar um site Wordpress, para que o time de Marketing Digital possa configurar o site principal da companhia. O Kubernetes é a solução oficial de orquestração dos containers da empresa. O MySQL é tecnologia de banco de dados principal, com um time de DBA especializados para sustentação. Foi solicitado o provisionamento do Wordpress, e um banco de dados MySQL de uso exclusivo do Wordpress, para persistência de todas as configurações realizadas pelo time de Marketing Digital. Tanto o Wordpress quanto o MySQL deverão estar em containers geridos pelo Kubernetes.

Para isso, você deverá criar todas as configurações Kubernetes necessárias para provisionamento do Wordpress e MySQL, utilizando alguma plataforma para execução de clusters Kubernetes, como microk8s, k3s, EKS da AWS, GKE do Google Cloud (GCP), entre outros, permitindo instanciar todos pods, services, ingress e configurações adicionais necessárias, garantindo que mesmo ao destruir um pod Wordpress e/ou MySQL, os dados de configuração do ambiente Wordpress não sejam perdidos.

## Checklist de entrega
Ao final deste cenário, você deverá ter conseguido atingir os objetivos a seguir:
1. **Configuração do Kubernetes**:
    - [ ]     Criação dos arquivos YAML para deployment do Wordpress e MySQL.
    - [ ]     Configuração de Persistent Volume Claims (PVCs) para garantir a persistência dos dados.
    - [ ]     Definição dos Services e Ingress para exposição do Wordpress.
2. **Testes de Resiliência**:
    - [ ]     Simulação da perda de pods para testar a recuperação automática dos serviços.
    - [ ]     Verificação da integridade dos dados após a recuperação dos pods.
4. **Scripts de IaC/Kustomize**:
    - [ ]     Desenvolvimento de scripts de Infraestrutura como Código, se aplicável.
    - [ ]     Teste dos scripts/módulos Kustomize para assegurar a correta funcionalidade.