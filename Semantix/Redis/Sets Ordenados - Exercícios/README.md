# Exercícios - Sets Ordenados

1. Deletar a chave "pesquisa:produto"

        del pesquisa:produto

2. Criar a chave "pesquisa:produto" do tipo set ordenado com os seguintes valores:

Valor: monitor, Score: 100

        zadd pesquisa:produto 100 monitor
        
Valor: HD, Score: 20
Valor: mouse, Score: 10
Valor: teclado, Score: 50
O score representa a quantidade de pesquisas feitas para aquele produto na aplicação

        -- pode adicionar um ao lado do outro para ficar em um único comando
        zadd pesquisa:produto 20 HD 10 mouse 50 teclado

1. Visualizar a quantidade de produtos

        zcard pesquisa:produto

2. Visualizar todos os produtos do mais pesquisado ao menos pesquisado

        zrevrange pesquisa:produto 0 -1
        
        -- o mais pesquisado é o produto com maior score. Já que score é o número de pesquisas em nosso contexto
        -- a diferença está no comando inicial. Usamos o zrevrange para descrecente. Ordem crescente seria zrange

3. Visualizar o rank do produto teclado

        zrevrank pesquisa:produto teclado
        
        -- usando o rev pelo mesmo contexto, de mais pesquisados

4. Visualizar o score do produto teclado

        zscore pesquisa:produto teclado

5. Remover o valor HD da chave

        zrem pesquisa:produto HD

6. Recuperar e remover do set o produto mais pesquisado

        zpopmax pesquisa:produto 

7. Recuperar e remover do set o produto menos pesquisado

        zpopmin pesquisa:produto

8. Visualizar todos os produtos

        zrange pesquisa:produto 0 -1
        
