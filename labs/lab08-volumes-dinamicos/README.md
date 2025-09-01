## Lab 8: Armazenamento com Provisionamento Dinâmico

 ### Objetivo
 Aprender a usar o provisionamento dinâmico de volumes, onde um `PersistentVolume` é criado automaticamente para atender a um `PersistentVolumeClaim`, eliminando a necessidade de o administrador pré-provisionar o armazenamento.

 ### Conceitos Chave
 * **StorageClass:** Um objeto que descreve um "tipo" de armazenamento oferecido. Ele define qual provisionador de volume usar e os parâmetros para esse provisionador. Quando um PVC especifica um StorageClass, ele aciona o provisionamento dinâmico.
 * **Provisioner:** O componente de backend que efetivamente cria o armazenamento físico. O Docker Desktop vem com um provisionador `hostpath` por padrão.

 ### Passos Executados
 1. **Criação do PVC:** Criamos um PVC (`pvc-dynamic.yaml`) que, em vez de esperar por um PV existente, especificou o `storageClassName: hostpath`.
    ```bash
    kubectl apply -f pvc-dynamic.yaml
    ```
 2. **Verificação da Magia:** Imediatamente após a criação do PVC, verificamos que:
    * O PVC já estava com status `Bound`.
    * Um **novo PV foi criado automaticamente** pelo Kubernetes para satisfazer a reivindicação.
    ```bash
    kubectl get pvc
    kubectl get pv
    ```
 3. **Consumo e Limpeza:** Os Pods consumiram o PVC normalmente. Na limpeza, ao deletar o PVC, o PV provisionado dinamicamente também foi deletado automaticamente, graças à política `reclaimPolicy: Delete` definida no StorageClass.
