# Comando Básicos para BD, Collections e Documentos

1. Criar o banco de dados com seu nome.

        use jader

2. Listar os banco de dados.

        show dbs

3. Criar a collection produto no bd com seu nome.

        -- dica. Se digitarmos db. e depois dar um TAB, podemos ver todas as funções
        -- ele é autocomplete com o TAB
        -- se não souber os parâmetros, pode apagar os parenteses e dar um entre que ele mostra as opç

        db.createCollection('produto')

4. Listar os banco de dados.

        show dbs

5. Listar as collections.

        show collections

6. Inserir os seguintes documentos na collection produto:

- _id: 1, "nome": “cpu i5", "qtd": "15“

        db.produto.insertOne({ _id: 1, nome: "cpu i5", qtd: 15})      
- _id: 2, nome: “memória ram", qtd: 10, descricao: {armazenamento: “8GB”, tipo:“DDR4“}

        db.produto.insertOne({ _id: 2, nome: "memória ram", qtd: 10, descricao: {armazenamento: "8GB", tipo: "DDR4"}})
- _id: 3, nome: "mouse", qtd: 50, descricao: {conexao: “USB”, so: [“Windows”, “Mac”, “Linux“]}

        db.produto.insertOne({ _id: 3, nome: "mouse", qtd: 50, descricao: {conexao: "USB", so: ["Windows", "Mac", "Linux"]}})
- _id: 4, nome: “hd externo", "qtd": 20, descricao: {conexao: “USB”, armazenamento: “500GB”, so: [“Windows 10”, “Windows 8”, “Windows 7”]}

        db.produto.insertOne({ _id: 4, nome: "hd externo", qtd: 20, descricao: {conexao: "USB", armazenamento: "500GB", so: ["Windows", "Mac", "Linux"]}})

7. Mostrar todos os documentos.

        -- para mostrar a estrutura completa e identado
        db.produto.find().pretty()
        
        -- mas se quiser uma consulta tápida em uma linha, pode colocar até o find()
        db.produto.find()
        
8.  Pesquisar na collection produto, os documentos com os seguintes atributos:

- a) Nome = mouse

        db.produto.find({nome: "mouse"})

- b) Quantidade = 20 e apresentar apenas o campo nome

        db.produto.find({qtd: {$eq: 20}}, {nome: 1, _id: 0})

- c) Quantidade <= 20 e apresentar apenas os campos nome e qtd

       db.produto.find({qtd: {$lte: 20}}, {nome: 1,qtd: 1,_id: 0})

- d) Quantidade entre 10 e 20

      db.produto.find({qtd: {$gte: 10, $lte: 20}})

- e) Conexão = USB e não apresentar o campo _id e qtd

      -- para pesquisar dentro das chaves, obrigatoriamente precisa usar as aspas 
      db.produto.find({'descricao.conexao': "USB"},{_id: 0, qtd: 0})

- f) SO que contenha “Windows” ou “Windows 10”

      db.produto.find({'descricao.so': {$in: ["Windows", "Windows 10" ]}})

