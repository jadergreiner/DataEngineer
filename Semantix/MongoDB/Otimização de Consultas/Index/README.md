# Index e plano de execução

1. Mostrar todos os documentos da collection produto do banco de dados seu nome

        db.produto.find()

2. Criar o index “query_produto” para pesquisar o campo nome do produto em ordem alfabética

       -- sintaxe
       -- db.produto.CreateIndex({},{})
       -- primeira chave é o campo escolhido e a segunda chave é o nome
       -- quero pesquisar pelo nome em ordem alfabética. Se fosse descrescente seria -1
       db.produto.CreateIndex({nome: 1},{name: "query_produto"})

3. Pesquisar todos os índices da collection produto

4. Pesquisar todos os documentos da collection produto

5. Visualizar o plano de execução do exercício 4

6. Pesquisar todos os documentos da collection produto, com uso da index “query_produto”

7. Visualizar o plano de execução do exercício 7

8. Remover o index “query_produto”

9. Pesquisar todos os índices da collection produto
