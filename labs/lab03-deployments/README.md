## Lab 3: Gerenciamento de Deployments

### Objetivo
Aprender a utilizar o objeto `Deployment`, um recurso de mais alto nível que gerencia o ciclo de vida dos Pods de forma declarativa. Deployments automatizam a implantação, o escalonamento e as atualizações de aplicações.

### Conceitos Chave
* **Deployment:** Gerencia um conjunto de Pods idênticos, garantindo que um número específico de réplicas esteja sempre em execução.
* **ReplicaSet:** Um objeto de nível mais baixo, controlado pelo Deployment, cuja única função é manter um número estável de réplicas de Pods.
* **Rolling Update:** A estratégia padrão de atualização do Deployment, que atualiza os Pods gradualmente, substituindo instâncias antigas por novas sem causar indisponibilidade no serviço.

### Passos Executados

1.  **Criação do Deployment:** Criamos um Deployment que especifica `3 réplicas` de um Pod com a imagem `kube-test-container:v1.0`.
    ```bash
    kubectl apply -f my-deployment.yaml
    ```
2.  **Disparando um Rollout:** Editamos o arquivo `my-deployment.yaml`, alterando a tag da imagem para `v1.1`. Ao reaplicar o arquivo, o Kubernetes iniciou uma "rolling update" para atualizar a aplicação.
    ```bash
    # (Após editar o arquivo)
    kubectl apply -f my-deployment.yaml

    # Acompanhamos o progresso da atualização
    kubectl rollout status deployment my-deployment
    ```
3.  **Escalonamento:** Aumentamos o número de réplicas de 3 para 5 com um comando direto.
    ```bash
	kubectl scale deployment my-deployment --replicas=5
    ```

