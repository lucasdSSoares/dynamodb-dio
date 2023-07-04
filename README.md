# Desafio DIO DynamoDB

Ao utilizar o DynamoDB, você pode começar criando uma tabela, especificando seu nome, as chaves de partição e opcionalmente uma chave de classificação. As chaves de partição são usadas para distribuir os dados por diferentes nós de armazenamento e as chaves de classificação são usadas para ordenar os itens dentro de cada partição. Em seguida, você pode inserir dados na tabela utilizando o comando `put-item`, onde você especifica os atributos e seus respectivos valores. O DynamoDB é flexível em termos de esquema, permitindo que diferentes itens tenham diferentes atributos.

Além disso, você pode criar índices no DynamoDB para melhorar a eficiência das consultas. Existem dois tipos principais de índices: índices globais e índices locais. Os índices globais permitem que você consulte dados em qualquer atributo da tabela, enquanto os índices locais permitem consultas apenas em atributos específicos. Você pode criar e atualizar índices através da definição de atributos de chave e projeções de atributos. Isso permite que você consulte os dados de forma mais eficiente, acessando diretamente os itens relevantes sem precisar percorrer a tabela inteira.



### Serviço utilizado

Amazon DynamoDB

Amazon CLI para execução em linha de comando

Linux Ubuntu 

Gitbash



### Comandos para execução do experimento:

*
