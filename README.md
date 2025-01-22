# Fake Shop CI/CD Pipeline com Kubernetes e AWS

Este projeto implementa uma aplicação web chamada Fake Shop, que é implantada em um cluster Kubernetes na AWS. A infraestrutura é provisionada e gerenciada via CI/CD utilizando GitHub Actions.

## Visão Geral do Projeto

A Fake Shop é uma aplicação fictícia composta por:

- **Backend e banco de dados:**
  - Um banco PostgreSQL que armazena dados da aplicação.
  - Uma aplicação web desenvolvida com Flask.

- **Monitoramento:**
  - Coleta de métricas do cluster e da aplicação usando Prometheus e Grafana.

- **Pipeline CI/CD:**
  - Constrói, envia e implanta a aplicação automaticamente no cluster Kubernetes.

## Estrutura do Projeto

### Kubernetes Manifests

- **Banco de Dados PostgreSQL:**
  - Um Deployment gerencia um pod rodando o PostgreSQL.
  - Um Service expõe o banco na porta 5432.

- **Aplicação Fake Shop:**
  - Um Deployment gerencia 4 réplicas da aplicação Flask.
  - Anotações para coleta de métricas foram adicionadas para Prometheus.
  - Um Service do tipo LoadBalancer expõe a aplicação.

### Pipeline CI/CD (main.yaml)

- **Etapa de CI:**
  - O código é clonado do repositório.
  - Uma imagem Docker da aplicação é construída e enviada para o Docker Hub.

- **Etapa de CD:**
  - O cluster EKS é configurado com kubectl.
  - Os manifestos do Kubernetes são aplicados.
  - A imagem mais recente da aplicação é implantada.

## Infraestrutura como Código (IaC) com Terraform

Para automatizar o provisionamento do cluster Kubernetes na AWS, este projeto inclui um arquivo Terraform que cria um cluster EKS.

### Estrutura do Terraform

- **Arquivo:**
  - `main.tf`: Define o provedor AWS, configuração de rede, e cria o cluster EKS.
  

### Etapas para Configuração

1. Instale o Terraform em sua máquina local.
2. Configure suas credenciais AWS com permissões para criar recursos (IAM, VPC, EKS, etc.).
3. Execute os seguintes comandos:

   ```bash
   terraform init
   terraform plan
   terraform apply

## Conectando ao Cluster EKS e Implantação

Assim que o provisionamento for concluído, conecte-se ao cluster EKS com o seguinte comando:

   ```bash
      aws eks update-kubeconfig --region <sua-região> --name <nome-do-cluster>
   ```

## Implantação e Configuração

1. **Implante os manifestos do Kubernetes no cluster.**

   ```bash
   kubectl apply -f <caminho-dos-manifestos>
   ```

### Configuração e Execução

#### Pré-requisitos

- **Docker Hub:** Configurar as credenciais no GitHub Secrets:

  ```plaintext
  DOCKERHUB_USERNAME: <seu-usuário>
  DOCKERHUB_TOKEN: <seu-token>
  ```

- **AWS EKS:** Criar um cluster EKS e configurar credenciais:

  ```plaintext
  AWS_ACCESS_KEY_ID: <sua-access-key>
  AWS_SECRET_ACCESS_KEY: <sua-secret-key>
  AWS_SECRET_REGION: <sua-região>
  ```

- **GitHub Actions:** Certifique-se de que as permissões do repositório estejam habilitadas para CI/CD.

### Deploy na AWS

1. Garanta que seu cluster EKS esteja ativo e configurado.
2. Faça push para o branch main para acionar o pipeline CI/CD:

   ```bash
   git add .
   git commit -m "Atualizando projeto"
   git push origin main
   ```

3. Acompanhe a execução no GitHub Actions.

## Melhorias Futuras

- Implementação de um sistema de mensagens para registrar eventos.
- Configuração de mais dashboards personalizados no Grafana.




