## Lab 1: Criação de Pods - Interativa vs. Declarativa

### Objetivo
Compreender as duas formas primárias de criar recursos no Kubernetes: a interativa (imperativa), útil para testes rápidos, e a declarativa, a prática recomendada para ambientes de produção que permite o versionamento de infraestrutura (GitOps).

### Conceitos Chave
* **Pod:** A menor unidade computacional do Kubernetes. Um Pod encapsula um ou mais contêineres, armazenamento e opções de rede.

### Passos Executados

#### 1. Criação de Pod - Modo Interativo
A abordagem imperativa envolve dar ordens diretas ao cluster através de comandos.

```bash
# Este comando cria um Pod chamado 'my-nginx' de forma direta.
# A flag --restart=Never assegura que o Kubernetes crie um objeto Pod,
# em vez de um objeto de mais alto nível como um Deployment.
kubectl run my-nginx --image=nginx --restart=Never

# Verificamos se o Pod foi criado e está no estado 'Running'.
kubectl get pods

'''

apiVersion: v1
kind: Pod
metadata:
  name: my-nginx-pod
spec:
  containers:
  - name: nginx
    image: nginx

# O comando 'apply' lê o manifesto e instrui o Kubernetes
# a criar ou atualizar os recursos para que correspondam ao estado declarado no arquivo.
kubectl apply -f my-nginx-pod.yaml

Conclusão
Este laboratório demonstrou a diferença fundamental entre as abordagens imperativa e declarativa. Enquanto a primeira é rápida para testes, a segunda é robusta, repetível e essencial para a automação e o gerenciamento de infraestrutura como código.
