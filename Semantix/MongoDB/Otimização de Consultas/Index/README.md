# Index e plano de execução

1. Mostrar todos os documentos da collection produto do banco de dados seu nome

        db.produto.find()

2. Criar o index “query_produto” para pesquisar o campo nome do produto em ordem alfabética

       -- sintaxe
       -- db.produto.CreateIndex({},{})
       -- primeira chave é o campo escolhido e a segunda chave é o nome
       -- quero pesquisar pelo nome em ordem alfabética. Se fosse descrescente seria -1
       db.produto.createIndex({nome: 1},{name: "query_produto"})

3. Pesquisar todos os índices da collection produto

        db.produto.getIndexes()

4. Pesquisar todos os documentos da collection produto

        db.produto.find()

5. Visualizar o plano de execução do exercício 4

        db.produto.find().explain()
        
        --winningPlan COLLSCAN. Ou seja, plano vencedor COLLSCAN vare todas as colunas

6. Pesquisar todos os documentos da collection produto, com uso da index “query_produto”

        db.produto.find().hint({nome: 1})

7. Visualizar o plano de execução do exercício 6

        db.produto.find().hint({nome: 1}).explain()
        -- a ordenação agora é pelo nome
        - o winningPlan é FETCH e um stage IXSCAN
        - por aqui verificamos que ele não está varrendo todos os dados. Está varrendo apenas pelo seu índice

8. Remover o index “query_produto”

        db.produto.dropIndex({nome:1})

9. Pesquisar todos os índices da collection produto

        db.produto.getIndexes()
