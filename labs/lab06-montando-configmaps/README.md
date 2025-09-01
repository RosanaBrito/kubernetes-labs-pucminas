## Lab 6: Consumindo ConfigMaps em Pods

 ### Objetivo
 Aprender as duas principais formas de um Pod consumir dados de um `ConfigMap`: como variáveis de ambiente e como arquivos montados em um volume.

 ### Passos Executados

 Após implantar uma aplicação de API e um banco de dados MongoDB, realizamos duas modificações no `Deployment` da API.

 1.  **Injetando como Variável de Ambiente:**
     * Editamos o `Deployment` com `kubectl edit deployment apitool`.
     * Modificamos a definição da variável de ambiente `MONGO_URI`. Em vez de um valor fixo (`value`), usamos `valueFrom` para instruir o Kubernetes a buscar o valor da chave `MONGO_URI` dentro do ConfigMap `apitool-conf`.
     * Isso desacoplou a string de conexão do banco de dados da definição do Pod.

     **Trecho do YAML (antes):**
     ```yaml
     env:
     - name: MONGO_URI
       value: "mongodb://mongodb:27017/my_database"
     ```
     **Trecho do YAML (depois):**
     ```yaml
     env:
     - name: MONGO_URI
       valueFrom:
         configMapKeyRef:
           name: apitool-conf
           key: MONGO_URI
     ```

 2.  **Montando como Volume:**
     * Editamos o `Deployment` novamente.
     * Adicionamos uma seção `volumes` na especificação do Pod, que referencia o ConfigMap `apitool-schemas`.
     * Adicionamos uma seção `volumeMounts` na definição do contêiner, que monta o volume `schemas` no diretório `/app/schemas`.
     * Como resultado, as chaves do ConfigMap (`users.json`, `products.json`) tornaram-se arquivos dentro do contêiner, que foram lidos pela aplicação para configurar suas coleções.
