## Lab 5: Criação Avançada de ConfigMaps

 ### Objetivo
 Aprender formas alternativas e práticas de criar `ConfigMaps`, utilizando arquivos externos e valores literais diretamente na linha de comando.

 ### Passos Executados

 1.  **Criando a partir de Arquivos:** Utilizamos o comando `kubectl create configmap` com a flag `--from-file` para criar um ConfigMap (`apitool-schemas`) cujo conteúdo das chaves é preenchido com o conteúdo de arquivos `.json`.
     * O `dry-run=client -o yaml` foi usado para gerar o manifesto YAML sem aplicá-lo, permitindo-nos inspecionar e salvar o arquivo antes da criação.
     ```bash
     kubectl create configmap apitool-schemas \
       --from-file=path/to/users.json \
       --from-file=path/to/products.json \
       --dry-run=client -o yaml > api-schemas.yaml

     kubectl apply -f api-schemas.yaml
     ```

 2.  **Criando a partir de Valores Literais:** Usamos a flag `--from-literal` para criar um ConfigMap (`apitool-conf`) com pares chave-valor definidos diretamente no comando. Ideal para configurações simples, como URLs de conexão.
     ```bash
     kubectl create configmap apitool-conf \
       --from-literal=MONGO_URI=mongodb://mongodb.default.svc:27017/my_database \
       --dry-run=client -o yaml > apitool-conf.yaml

     kubectl apply -f apitool-conf.yaml
     ```
