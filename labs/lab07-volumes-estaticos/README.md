## Lab 7: Armazenamento com Provisionamento Estático

 ### Objetivo
 Compreender o ciclo de vida do armazenamento persistente no Kubernetes através do modelo de provisionamento estático, onde o administrador do cluster cria `PersistentVolumes` (PVs) que são então consumidos por `PersistentVolumeClaims` (PVCs) das aplicações.

 ### Conceitos Chave
 * **PersistentVolume (PV):** Um pedaço de armazenamento no cluster que foi provisionado por um administrador. É um recurso do cluster, assim como um nó.
 * **PersistentVolumeClaim (PVC):** Uma solicitação de armazenamento feita por um usuário/aplicação. Ela consome os recursos de um PV.
 * **Ciclo de Vida:** Um PV começa com status `Available`. Quando um PVC compatível o solicita, seu status muda para `Bound`. Quando o PVC é liberado, a política de recuperação (`ReclaimPolicy`) do PV determina o que acontece com o volume (se ele é retido, reciclado ou deletado).

 ### Passos Executados
 1. **Criação dos PVs:** Criamos dois PVs manualmente, definindo sua capacidade e modo de acesso.
    ```bash
    kubectl apply -f pre-provisioned.yaml
    kubectl get pv # Status: Available
    ```
 2. **Criação do PVC:** Criamos um PVC que solicita 2Gi de armazenamento.
    ```bash
    kubectl apply -f pvc-2G.yaml
    ```
 3. **Verificação do "Binding":** O Kubernetes automaticamente "ligou" (Bound) o nosso PVC ao PV de 2Gi que estava disponível.
    ```bash
    kubectl get pv # Status do PV de 2Gi: Bound
    ```
 4. **Consumo do PVC:** Os Pods da aplicação foram configurados para usar o volume através do nome do PVC (`static-claim`), abstraindo completamente os detalhes do armazenamento físico subjacente.
    ```bash
    kubectl apply -f writer-pvc.yaml
    kubectl apply -f reader-pvc.yaml
    ```
