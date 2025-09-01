# Laboratórios de Kubernetes - Pós-Graduação DevOps PUC-Minas

## 📖 Sobre o Projeto

Este repositório contém a resolução dos laboratórios práticos da disciplina de orquestração de contêineres com Kubernetes, parte do curso de **Pós-Graduação em DevOps Continuous Engineering da PUC-Minas**.

O projeto demonstra de forma prática a aplicação de conceitos fundamentais e avançados do Kubernetes, desde a criação de Pods e Deployments até a configuração de volumes persistentes e controle de acesso (RBAC).

## 📂 Navegação dos Laboratórios

Este repositório é organizado em "capítulos", onde cada diretório representa um laboratório específico e contém tanto os manifestos `.yaml` quanto uma documentação detalhada daquela etapa.

Clique nos links abaixo para navegar para cada laboratório:

* **[Lab 01: Pods](./labs/lab01-pods/)** - *Criação de Pods de forma interativa e declarativa.*
* **[Lab 02: Sidecars e ConfigMaps](./labs/lab02-sidecars-configmaps/)** - *Uso do padrão sidecar e injeção de configurações com ConfigMaps.*
* **[Lab 03: Deployments](./labs/lab03-deployments/)** - *Gerenciamento do ciclo de vida de aplicações com Deployments, rollouts e escalonamento.*
* **[Lab 04: Services](./labs/lab04-services/)** - *Exposição de aplicações internamente no cluster com Services do tipo ClusterIP.*
* **[Lab 05: ConfigMaps Avançado](./labs/lab05-configmaps-avancado/)** - *Criação de ConfigMaps a partir de arquivos e valores literais.*
* **[Lab 06: Montando ConfigMaps](./labs/lab06-montando-configmaps/)** - *Consumo de ConfigMaps como variáveis de ambiente e volumes de arquivos.*
* **[Lab 07: Volumes Estáticos](./labs/lab07-volumes-estaticos/)** - *Gerenciamento de armazenamento com provisionamento estático (PV/PVC).*
* **[Lab 08: Volumes Dinâmicos](./labs/lab08-volumes-dinamicos/)** - *Provisionamento automático de volumes com StorageClasses.*
* **[Lab 09: RBAC (Controle de Acesso)](./labs/lab09-rbac/)** - *Implementação de permissões granulares para usuários e grupos.*

## 🛠️ Tecnologias Utilizadas

* **Orquestração:** Kubernetes
* **Ambiente Local:** Docker Desktop com WSL (Ubuntu)
* **Contêineres:** Docker
* **Manifestos:** YAML

## ✨ Agradecimentos

Agradeço ao incrível professor **Fernando Silva** por compartilhar seu vasto conhecimento e pela didática excepcional ao longo da disciplina.
