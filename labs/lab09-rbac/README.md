## Lab 9: Controle de Acesso Baseado em Função (RBAC)

 ### Objetivo
 Compreender e implementar o RBAC no Kubernetes para controlar o que diferentes usuários e grupos podem fazer dentro do cluster, seguindo o princípio do menor privilégio.

 ### Conceitos Chave
 * **Autenticação (AuthN):** O processo de verificar a identidade de um usuário ("Quem é você?"). Neste lab, usamos certificados de cliente.
 * **Autorização (AuthZ):** O processo de verificar se um usuário autenticado tem permissão para realizar uma ação ("O que você pode fazer?"). É aqui que o RBAC atua.
 * **Role / ClusterRole:** Objetos que contêm regras de permissão (verbos como `get`, `list`, `create` em recursos como `pods`, `services`). `Role` é para um único namespace, `ClusterRole` é para o cluster inteiro.
 * **RoleBinding / ClusterRoleBinding:** Objetos que "ligam" um `Role` ou `ClusterRole` a um `Subject` (um usuário, grupo ou service account).

 ### Passos Executados
 1. **Criação de Identidade (AuthN):** Usamos `openssl` para gerar uma chave privada e um Certificate Signing Request (CSR) para um usuário `puc-devops` no grupo `devs`. O CSR foi aprovado pelo cluster para gerar um certificado válido.
 2. **Configuração do `kubectl`:** Criamos um novo contexto no `kubeconfig` para que pudéssemos fazer requisições à API como o novo usuário `puc-devops`. Um teste inicial provou que o usuário não tinha nenhuma permissão.
 3. **Permissão de Namespace (`RoleBinding`):**
     * Criamos uma `Role` que permitia apenas ler (`get`, `list`) Pods.
     * **Desafio Encontrado:** O arquivo `RoleBinding` estava faltando no repositório.
     * **Solução:** Criamos o manifesto do `RoleBinding` manualmente para ligar a `Role` `pod-reader` ao usuário `puc-devops` dentro do namespace `default`. Isso permitiu ao usuário listar pods apenas nesse namespace.
 4. **Permissão de Cluster (`ClusterRoleBinding`):** Criamos uma `ClusterRoleBinding` para ligar uma `ClusterRole` que permite ler serviços a um `Group` (`devs`). Como nosso usuário pertence a esse grupo, ele herdou a permissão para listar serviços em todos os namespaces do cluster.
