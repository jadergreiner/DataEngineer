# Pesquisa e Paginação

### 1 . Pesquisar no índice produto os documentos com os seguintes atributos:

a) Nome = mouse

    GET produto/_search?q=nome:mouse
    
    -- ? = identação
    -- q= indica que é uma query
    --nome = nome do campo
    --mouse = essa é o valor que ele vai pesquisar

b) Quantidade = 30

    GET produto/_search?q=qtd:30

c) Descrição = USB

    GET produto/_search?q=descricao:USB

d) Nome = hd e descrição = windows

    GET produto/_search?q=nome:hd&q=descricao:windows
    
e) Nome = memória e descrição = GB

    GET produto/_search?q=nome:memoria&q=descricao:GB
    
    -- aqui não retorna por o "GB" está colado no nome. Mas podemos usar o "*" como buscar no texto
    GET produto/_search?q=nome:memoria&q=descricao:*GB

### 2 . Pesquisar todos os índices, limitando a pesquisa em 5 documentos em cada página e visualizar a 4 página (Documentos entre 16 á 20 )

    GET _all/_search?&size=5&from=15
