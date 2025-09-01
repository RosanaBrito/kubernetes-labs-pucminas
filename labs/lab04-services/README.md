## Lab 4: Expondo Aplicações com Services

 ### Objetivo
 Aprender a expor um conjunto de Pods (gerenciados por um Deployment) como um serviço de rede com um ponto de acesso único e estável dentro do cluster, utilizando o objeto `Service`.

 ### Conceitos Chave
 * **Service:** Um objeto que define uma política de acesso a um grupo de Pods. Ele fornece um endereço IP e uma porta de DNS estáveis, que não mudam mesmo que os Pods por trás dele sejam recriados.
 * **ClusterIP:** O tipo de serviço padrão, que expõe o serviço em um endereço IP interno ao cluster, tornando-o acessível apenas por outros componentes dentro do mesmo cluster.
 * **Selector:** O mecanismo que o Service usa para encontrar quais Pods ele deve direcionar o tráfego, baseado nas `labels` dos Pods.
 * **Endpoints:** A lista de endereços IP e portas reais dos Pods que correspondem ao seletor do Service. O Kubernetes mantém essa lista atualizada automaticamente.

 ### Passos Executados
 1. **Criação do Serviço:** Criamos um serviço do tipo `ClusterIP` chamado `my-svc` que seleciona os Pods com a label `app=myapp`.
    ```bash
    # Comando "one-liner" para criar o serviço e injetar o seletor correto
    kubectl create service clusterip my-svc --tcp '8000:8000' -o yaml --dry-run=client | \
    kubectl set selector --local -f - 'app=myapp' -o yaml | \
    kubectl create -f -
    ```
 2. **Verificação Interna:** Testamos o acesso ao serviço de *dentro* do cluster, executando um comando a partir de outro Pod.
    * **Desafio Encontrado:** A imagem do pod de teste (`kube-test-container`) era minimalista e não continha as ferramentas `curl` ou `wget`.
    * **Solução:** Utilizamos uma técnica de depuração comum: lançamos um pod de diagnóstico temporário (`busybox`) que possui as ferramentas necessárias para realizar o teste de rede.
    ```bash
    # Lançando o pod de diagnóstico
    kubectl run -it --rm --image=busybox temporary-pod -- sh

    # De dentro do pod, testando o serviço pelo seu nome de DNS
    / # wget -qO- http://my-svc:8000
    ```
 3. **Verificação Externa (`port-forward`):** Criamos um túnel de comunicação seguro da nossa máquina local para o serviço dentro do cluster.
    ```bash
    # Cria o túnel em background
    kubectl port-forward svc/my-svc 8080:8000 &

    # Testa o acesso através da porta local
    curl http://localhost:8080
    ```
