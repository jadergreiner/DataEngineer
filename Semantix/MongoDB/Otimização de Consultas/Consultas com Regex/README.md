# Consultas com Regex

1. Mostrar todos os documentos da collection produto do banco de dados seu nome

        db.produto.find()

2. Buscar os documentos com o atributo nome,  que contenham a palavra “cpu”

        -- se realizarmos a pesquisa tradicional não retornada nada
        -- nosso dado se chama cpu i7
        db.produto.find({nome: "cpu"})
        
        -- agora vamos aplicar o operador regex
        db.produto.find({nome: {$regex: "cpu"}})
        
        -- o padrao trabalhando com regex é o uso da / (barra)
        db.produto.find({nome: {$regex: /cpu/}})

3. Buscar os documentos  com o atributo nome, que começam por “hd” e apresentar os campos nome e qtd

        --para começar, usamos o ^
        db.produto.find({nome: {$regex: /^hd/}}, {_id: 0, nome: 1, qtd: 1})

4. Buscar os documentos  com o atributo descricao.armazenamento, que terminam com “GB” ou “gb” e apresentar os campos nome e descricao

        -- o "i" depois do nome é para deixar de ser case sensitive, ou seja, vai procurar maisculas ou mínusculas
        db.produto.find({"descricao.armazenamento": {$regex: /gb/i}"},{_id, nome: 1,  descricao: 1})

5. Buscar os documentos  com o atributo nome, que contenha a palavra memória, ignorando a letra “o”

        -- usaremos um caracter coringa (.) 'ponto'. Em nosso caso,tanto faz se tiver acento ou não ou qualquer outro caracter no campo
        db.produto.find({nome: {$regex: /mem.ria/i}})
        
        -- serve inclusive para pesquisar outros padrões
        db.produto.find({nome: {$regex: /.em./i}})
        db.produto.find({nome: {$regex: /m.mó./i}})
        db.produto.find({nome: {$regex: /.ria./i}})

6. Buscar os documentos  com o atributo qtd  que contenham valores com letras, ao invés de números.

        db.produto.find({qtd: {$regex: /[a-z]/}})

7. Buscar os documentos com o atributo descricao.sistema, que tenha exatamente a palavra “Windows”

        db.produto.find({"descricao.sistema": "Windoews"})
        -- nem sempre é necessário usar o REGEX
