# Fake Shop CI/CD Pipeline com Kubernetes e AWS

Este projeto implementa uma aplicação web chamada **Fake Shop**, que é implantada em um cluster Kubernetes na AWS. A infraestrutura é provisionada e gerenciada via CI/CD utilizando GitHub Actions.

## Visão Geral do Projeto

A Fake Shop é uma aplicação fictícia composta por:

1. **Backend e banco de dados:**
   - Um banco PostgreSQL que armazena dados da aplicação.
   - Uma aplicação web desenvolvida com Flask.

2. **Monitoramento:**
   - Coleta de métricas do cluster e da aplicação usando Prometheus e Grafana.

3. **Pipeline CI/CD:**
   - Constrói, envia e implanta a aplicação automaticamente no cluster Kubernetes.

## Estrutura do Projeto

### Kubernetes Manifests

1. **Banco de Dados PostgreSQL:**
   - Um `Deployment` gerencia um pod rodando o PostgreSQL.
   - Um `Service` expõe o banco na porta 5432.

2. **Aplicação Fake Shop:**
   - Um `Deployment` gerencia 4 réplicas da aplicação Flask.
   - Anotações para coleta de métricas foram adicionadas para Prometheus.
   - Um `Service` do tipo `LoadBalancer` expõe a aplicação.

### Pipeline CI/CD (main.yaml)

1. **Etapa de CI:**
   - O código é clonado do repositório.
   - Uma imagem Docker da aplicação é construída e enviada para o Docker Hub.

2. **Etapa de CD:**
   - O cluster EKS é configurado com `kubectl`.
   - Os manifestos do Kubernetes são aplicados.
   - A imagem mais recente da aplicação é implantada.

## Configuração e Execução

### Pré-requisitos

- **Docker Hub:** Configurar as credenciais no GitHub Secrets (`DOCKERHUB_USERNAME`, `DOCKERHUB_TOKEN`).
- **AWS EKS:** Criar um cluster EKS e configurar credenciais (`AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, `AWS_SECRET_REGION`).
- **GitHub Actions:** Certifique-se de que as permissões do repositório estejam habilitadas para CI/CD.

### Deploy na AWS

1. **Garanta que seu cluster EKS esteja ativo e configurado.**
2. **Faça push para o branch main para acionar o pipeline CI/CD..**
3. **Acompanhe a execução no GitHub Actions.**

### Melhorias Futuras

1. **Implementação de um sistema de mensagens para registrar eventos.**
2. **Configuração de mais dashboards personalizados no Grafana.**
3. **Automação do provisionamento do cluster Kubernetes na infraestrutura AWS**

