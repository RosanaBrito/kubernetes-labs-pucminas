## Lab 1: Criação de Pods - Interativa vs. Declarativa

### Objetivo
Compreender as duas formas primárias de criar recursos no Kubernetes: a interativa (imperativa), útil para testes rápidos, e a declarativa, a prática recomendada para ambientes de produção que permite o versionamento de infraestrutura (GitOps).

### Conceitos Chave
* **Pod:** A menor unidade computacional do Kubernetes. Um Pod encapsula um ou mais contêineres, armazenamento e opções de rede.

### Roteiro de Execução
O roteiro a seguir demonstra o processo completo do laboratório em um fluxo contínuo, com cada comando explicado através de comentários.

```bash
# --- PARTE 1: MODO INTERATIVO (IMPERATIVO) ---

# Passo 1.1: Criar um Pod diretamente via linha de comando.
# O comando 'kubectl run' é usado para criar rapidamente um recurso.
# A flag '--restart=Never' é crucial para garantir que um objeto 'Pod' seja
# criado, em vez de um 'Deployment'.
kubectl run my-nginx --image=nginx --restart=Never

# Passo 1.2: Verificar se o Pod foi criado com sucesso.
# O comando 'get pods' lista os Pods no namespace atual e seu status.
kubectl get pods
# Saída esperada: my-nginx ... Running

# --- PARTE 2: MODO DECLARATIVO ---

# Passo 2.1: Criar o arquivo de manifesto YAML.
# Em um cenário real, criaríamos este arquivo manualmente. Para fins de documentação,
# usamos o comando 'cat' para gerar o arquivo 'my-nginx-pod.yaml'.
cat <<EOF > my-nginx-pod.yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-nginx-pod
spec:
  containers:
  - name: nginx
    image: nginx
EOF

# Passo 2.2: Aplicar o manifesto no cluster.
# O comando 'kubectl apply -f' é a base da abordagem declarativa.
# Ele instrui o Kubernetes a fazer o estado do cluster corresponder ao
# estado descrito no arquivo.
kubectl apply -f my-nginx-pod.yaml

# Passo 2.3: Verificar novamente, agora vendo os dois Pods.
kubectl get pods
# Saída esperada: my-nginx ... Running
#                 my-nginx-pod ... Running

# --- PARTE 3: LIMPEZA ---

# Passo 3.1: Remover os recursos criados para manter o ambiente limpo.
kubectl delete pod my-nginx
kubectl delete -f my-nginx-pod.yaml
