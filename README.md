# Desafio DIO DynamoDB

Ao utilizar o DynamoDB, você pode começar criando uma tabela, especificando seu nome, as chaves de partição e opcionalmente uma chave de classificação. As chaves de partição são usadas para distribuir os dados por diferentes nós de armazenamento e as chaves de classificação são usadas para ordenar os itens dentro de cada partição. Em seguida, você pode inserir dados na tabela utilizando o comando `put-item`, onde você especifica os atributos e seus respectivos valores. O DynamoDB é flexível em termos de esquema, permitindo que diferentes itens tenham diferentes atributos.

Além disso, você pode criar índices no DynamoDB para melhorar a eficiência das consultas. Existem dois tipos principais de índices: índices globais e índices locais. Os índices globais permitem que você consulte dados em qualquer atributo da tabela, enquanto os índices locais permitem consultas apenas em atributos específicos. Você pode criar e atualizar índices através da definição de atributos de chave e projeções de atributos. Isso permite que você consulte os dados de forma mais eficiente, acessando diretamente os itens relevantes sem precisar percorrer a tabela inteira.



### Serviço utilizado

Amazon DynamoDB

Amazon CLI para execução em linha de comando

Linux Ubuntu 

Gitbash



### Comandos para execução do experimento:

* Criar uma tabela de Clientes

  ```
  aws dynamodb create-table \
      --table-name Clientes \
      --attribute-definitions \
          AttributeName=Cpf,AttributeType=S \
          AttributeName=Nome,AttributeType=S \
      --key-schema \
          AttributeName=Cpf,KeyType=HASH \
          AttributeName=Nome,KeyType=RANGE \
      --provisioned-throughput \
          ReadCapacityUnits=10,WriteCapacityUnits=5	`
  ```

  

* Inserir um item em massa

  > ```json
  > aws dynamodb batch-write-item \
  >     --request-items file://batchclientes.json
  > ```
  >
  > 

* Criar um index global secundário baseado na cidade.

  ```json
  aws dynamodb update-table \
      --table-name Clientes \
      --attribute-definitions AttributeName=Cidade,AttributeType=S \
      --global-secondary-index-updates \
          "[{\"Create\":{\"IndexName\": \"Cidade-index\",\"KeySchema\":[{\"AttributeName\":\"Cidade\",\"KeyType\":\"HASH\"}], \
          \"ProvisionedThroughput\": {\"ReadCapacityUnits\": 10, \"WriteCapacityUnits\": 5      },\"Projection\":{\"ProjectionType\":\"ALL\"}}}]"
  ```

- Criar um index global secundário baseado no nome do cliente e ano de nascimento

  ```json
  aws dynamodb update-table \    
      --table-name Clientes \
      --attribute-definitions\
          AttributeName=Nome,AttributeType=S \
          AttributeName=DataNasc,AttributeType=S \
      --global-secondary-index-updates \
          "[{\"Create\":{\"IndexName\": \"NomeDatanasc-index\",\"KeySchema\":[{\"AttributeName\":\"Nome\",\"KeyType\":\"HASH\"}, {\"AttributeName\":\"DataNasc\",\"KeyType\":\"RANGE\"}], \
          \"ProvisionedThroughput\": {\"ReadCapacityUnits\": 10, \"WriteCapacityUnits\": 5      },\"Projection\":{\"ProjectionType\":\"ALL\"}}}]"
  ```

- Pesquisar item por Cidade

  ```  json
  aws dynamodb query \
      --table-name Clientes \
      --key-condition-expression "Cidade = :cidade" \
      --expression-attribute-values  '{":cidade":{"S":"Salvador"}}'
  ```

  * Pesquisar item por Cpf e Data de Nascimento

  ``` json
   aws dynamodb query \
      --table-name Clientes \
      --key-condition-expression "Cpf  = :cpf and DataNasc = :datanasc" \
      --expression-attribute-values file://keycondcli.json
  
  ```

  

  

