## Lab 2: Pod com Múltiplos Contêineres (Sidecar) e ConfigMap

### Objetivo
Explorar o padrão "sidecar", onde um contêiner auxiliar roda junto ao contêiner principal para estender sua funcionalidade, e aprender a injetar configurações em Pods utilizando um `ConfigMap` como um volume de arquivos.

### Conceitos Chave
* **Sidecar Pattern:** Um padrão de design onde um contêiner auxiliar é implantado no mesmo Pod que o contêiner principal para adicionar funcionalidades, como logging, monitoramento ou proxy de rede. Ambos compartilham o mesmo ciclo de vida e rede.
* **ConfigMap:** Um objeto da API que armazena dados de configuração não sensíveis em pares chave-valor, desacoplando a configuração da imagem do contêiner.
* **Volume:** Um diretório contendo dados, acessível aos contêineres em um Pod. Neste lab, o volume é preenchido com os dados de um ConfigMap, que se tornam arquivos visíveis para o contêiner.

### Passos Executados

1.  **Criação do ConfigMap:** Primeiro, declaramos um ConfigMap contendo um bloco de configuração do Nginx.
    ```bash
    kubectl apply -f my-app-configmap.yaml
    ```
2.  **Criação do Pod:** Em seguida, criamos um Pod com dois contêineres: `myapp-container` (Nginx) e `sidecar-container` (BusyBox).
    * Na seção `volumes`, definimos um volume chamado `app-config` que obtém seu conteúdo do `ConfigMap` `my-app-config`.
    * Na seção `volumeMounts` do contêiner Nginx, montamos este volume no caminho `/etc/config`.
    ```bash
    kubectl apply -f myapp-pod.yaml
    ```
3.  **Verificação:** Verificamos se o arquivo do ConfigMap foi corretamente montado dentro do contêiner principal.
    ```bash
    kubectl exec myapp-pod -c my-app-container -- cat /etc/config/config-file
    ```
